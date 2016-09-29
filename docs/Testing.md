# Best practices for unit tests

The person writing the tests should be the same person writing the implementation. Ideally by writing tests first, see them fail, then change the implementation to make the test pass.
The test cases should be contained in the same commit as the corresponding implementation.
If test are written for existing legacy code, one good way to ensure all behaviour is covered is to intentionally introduce bugs in the code under test and see if it makes a test fail. If it does not, add an additional test case.
There should be an anonymous namespace around the test cases.
## Test names

Test names should be descriptive of the behaviour being tested. Use whole sentences with words sperated by underscores.
## Logic in tests 
Tests should not contain any logic ("if" statements).
Expected values should generally be constants and not be calculated.
## Use of mocks
Mocks are sort of a last resort, it is usually preferable to write code that is testable without the use of mocks.
If you still need a mock, create them using the gmock framework and don't try to implement them by hand.
Also in general if you need a mock that implements a particular interface there should already be such a mock ready to use in the same module that defines the interface. (In the "mock" subdirectory)
Generally most mocks should be strict mocks.
## Use of fixtures 
If there is common setup code for multiple test cases, place it in a fixture and declare tests using TEST_F(...)
If you don't need any common setup code, don't add an empty fixture and declare tests using TEST(...)
## Maximise the usefulness of the test output in case of failure
Write the expected value first.
```
EXPECT_EQ(expected, actual)
```
Sometimes it is useful to add extra output to failing expectations:
```
EXPECT_TRUE(...) << "something went wrong" << endl;
```
Avoid introducing intermediate variables for expected values:
```
// Bad:
const int value = someFunctionCall();
EXPECT_EQ(5, value);
  
// Better:
EXPECT_EQ(5, someFunctionCall());
  
// If absolutely unavoidable, at least give the intermediate value a meaningful name:
struct SomeStruct { ... };
const SomeStruct resultOfSomeFunctionCall = someFunctionCall();
EXPECT_EQ(5, resultOfSomeFunctionCall.a);
EXPECT_EQ(9, resultOfSomeFunctionCall.b);
```
Prefer EXPECT_* over ASSERT_* if the test case can continue without crashing. This will produce more output in the fail case and thus gives the programmer more clues on what went wrong. See EXPECT-VS-ASSERT.
Avoid expectation inside function calls:
```
// Bad:
void checkValue(int value)
{
    EXPECT_EQ(..., value);
}
  
TEST(...)
{
    const int someValue = ....;
    checkValue(someValue);
}
  
// Better:
TEST(...)
{
    const int someValue = ....;
    checkValue(someValue);
}
```

## Use an anonymous namespace for your tests
All your tests should be put in an anonymous namespace.
Rational
In order to avoid linker issues, we put tests in an anonymous namespace so the symbol names do not clash with others.
e.g.:
```
#include "gtest/gtest.h"
...
  
namespace {
  
  /** Your Tests go here! */
  
} // anonymous namespace
```

## Include Tests

For each component there has to be an include test, which is basically an empty test but it includes all header files of the component.
Rational
We want to have a accurate and complete reporting for our components. Because quite some tools (Klockwerk, Bullseye, etc.) rely on the fact that headers which shall be analysed are included in at least one test we need to have an include test.
e.g.:
```
#include file1.h
#include file2.h
...
  
#include "gtest/gtest.h"
  
namespace {
  
  TEST (include, test)
  {}
  
} // anonymous namespace
```
  
Include the Headers of your tested components first
Always include the headers of your tested components first in the test file.
Rational
Include issue might be found, which might be hidden due to test includes.

e.g.:
component header file did not include platform\stdint.h, but it the test fixture is included first and it also includes the platform/stdint.h the missing include issue will be hidden in the test.
