[Main Page](../README.md)

# Table of contents
* [Const Corectness](#const-corectness)
* [Includes](#includes)
* [Functions](#functions)
* [Comments](#comments)
* [Namespaces](#namespaces)
* [Null](#null)


## Const Corectness
Const should be used wherever possible. It makes an interfaces easier to use and offers potential for optimization to the compiler.

## Includes

The style used to specify an include shall reflect the locality of the included header file.

1. All includes which are part of the module the including header file is part of shall use quotes *""*
2. All includes which are not part of the module the including header (external includes) file is part of shall use angle brackets *<>*
3. Sort includes alphabetically
4. Put external includes after internal ones

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

//File: include/logger/BufferedLoggerOutput.h

#include "logger/EntryBuffer.h"
#include "logger/EntrySerializer.h"
#include "logger/IEntryOutput.h"
#include "logger/ILoggerListener.h"
#include "logger/ILoggerTime.h"
#include &lt;estd/forward_list.h&gt;
#include &lt;util/logger/IComponentMapping.h&gt;
#include &lt;util/logger/ILoggerOutput.h&gt;

</pre></td><td><pre lang="cpp">

//File: include/logger/BufferedLoggerOutput.h

#include "estd/forward_list.h"
#include "util/logger/IComponentMapping.h"
#include "util/logger/ILoggerOutput.h"
#include "logger/IEntryOutput.h"
#include "logger/ILoggerListener.h"
#include "logger/ILoggerTime.h"
#include "logger/EntryBuffer.h"
#include "logger/EntrySerializer.h"

</pre></td></tr>
</table>
**
### Summary
:white_check_mark: for module internal includes use quotes *""*

:white_check_mark: for module external includes use angle brackets *<>*

## Functions
### A function should perform a single logical operation
A function that performs a single operation is simpler to understand, test, and reuse.

### Keep functions short and simple
Large functions are hard to read, more likely to contain complex code, and more likely to have variables in larger than minimal scopes. 

Functions with complex control structures are more likely to be long and more likely to hide logical errors

"It doesn't fit on a screen" is often a good practical definition of "far too large." 

Break large functions up into smaller cohesive and named functions. Small simple functions are easily inlined where the cost of a function call is significant.

### For "in" parameters, pass cheaply-copied types by value and others by reference to const
Both let the caller know that a function will not modify the argument, and both allow initialization by rvalues.

What is "cheap to copy" depends on the machine architecture, but two or three words (doubles, pointers, references) are usually best passed by value. 

When copying is cheap, nothing beats the simplicity and safety of copying, and for small objects (up to two or three words) it is also faster than passing by reference because it does not require an extra indirection to access from the function.
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">
// pass by reference to const; always cheap
void f1(const string& s);  

// Unbeatable
void f3(int x);            

</pre></td><td><pre lang="cpp">
// potentially expensive
void f2(string s);         

// overhead on access in f4()
void f4(const int& x);

</pre></td></tr>
</table>

## Comments
Comments

Generally speaking, there shouldn't be many comments in source files. If you have to write comments for a piece of code, consider rewriting it so that it is easier to understand. Extracting inlined functions with speaking names might be one possible approach.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class Timeout 
{
    public:

    static const uint8_t MAX_TIMEOUT_IN_MS = 128U; 
    
    ...
};

</pre></td><td><pre lang="cpp">

class Timeout 
{
    public:

    static const uint8_t MAX_TIMEOUT = 128U; // unit is miliseconds
    
    ...
};

</pre></td></tr>
</table>
**

## Namespaces
Global namespaces and variables should always be referred to using the :: operator.
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

::common::io::getDigital();

</pre></td><td><pre lang="cpp">

common::io::getDigital();

</pre></td></tr>
</table>

### Summary
:white_check_mark: Try to encode all important information in the source code itself.

## NULL
Because the MACRO NULL can lead to incompatibility issues between C and C++ the literal 0L is used instead.

## Expressions with booleans

Never use the constants "true" or "false" as operands to "operator=="
or "operator !=". It makes the expressions unnecessary long and hard to
read.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

if (isGood) {
    ...
}

if (hasSomething && !isGood) {

}

</pre></td><td><pre lang="cpp">


if (true == isGood) {
    ...
}

if (true == ((true == hasSomething) && (false == isGood))) {
    ...
}

</pre></td></tr>
</table>
**

## Trivial if-else

Just don't do this, you are not paid per lines of code produced.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

return isGood;

</pre></td><td><pre lang="cpp">

if (isGood) {
    return true;
}
else {
    return false;
}

</pre></td></tr>
</table>
**

