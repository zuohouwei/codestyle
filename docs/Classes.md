[Main Page](../README.md)

# Classes

## Table of contents
* [Class Names](#class names)
* [Member Variable Names](#member variable names)
* [Getters, Setters, Attribute Functions](#getters, setters, attribute functions)
* [Class Invariant](#class invariant)
* [Avoid protected data](#avoid_protected_data)
* [Use class hierarchies to represent concepts with inherent hierarchical structure (only)](#)
* [Ordering](#ordering)
* [Declarations](#declarations)
* [Templates](#templates)

## Class Names
Class names are written in camel case starting with a capital letter. Also abbreviations like **CAN** are camel case: **Can**. 
_Interface names_ start prefixed with a capital **I**. Names of abstract classes are not treated specially any more, we used to prefix them with **Abstract**.

In unit tests, when writing a mock, the class name is usually postfixed with **Mock**.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td>
<pre lang="cpp">
class CanTransceiver;
class CanTransceiverMock;
class FilteredLinFrameListerner;
class ITransportMessageProvider; //interface
</pre>
</td><td>
<pre lang="cpp">
class CANTransceiver;
class filteredLINFrameListener;
class AbstractDiagJob; //should be DiagJob
</pre>
</td></tr>
</table>

### Summary
* Class names are CamelCase

## Member Variable Names
Member variables of a `class`, `struct` or `union` shall be prefixed. You will
find the prefix **f** a lot but also **m** or **_**. Don't invent any new
prefixes, postfixes are forbidden. Also, be consistent within your module, never
mix styles.

If a struct is used as a *POD*, i.e. all members are public and it does not
provide and functions, you can omit the prefix.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td>
<pre lang="cpp">

class CanTransceiver
{
    ::estd::forward_list<ICanFrameListener> fListeners;
};

struct Result
{
    ::bsp::ErrorCode status;
    uint16_t value;
};

</pre>
</td><td>
<pre lang="cpp">

class CanTransceiver
{
    ::estd::forward_list<ICanFrameListener> listeners;
};

struct Result
{
    ::bsp::ErrorCode Status;
    uint16_t value_;
};

</pre>
</td></tr>
</table>


## Getters, Setters, Attribute Functions
In general `set` functions should be avoided. Classes should be initialized
when calling their constructor. To read properties of a class, avoid `get`
functions, instead use `const` attribute style functions.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td>
<pre lang="cpp">

class CanTransceiver
{
public:
    CanTransceiver(BusId id);

    BusId busId() const;
};

</pre>
</td><td>
<pre lang="cpp">

class CanTransceiver
{
public:
    void setBusId(BusId id);

    BusId getBusId() const;
};

</pre>
</td></tr>
</table>

### Summary
* Function names are camelCase
* Boolean functions start with _is_ or _has_
* Consider signature part of name
* Getters should use attribute style

## Class Invariant
Use class if the class has an invariant; use struct if the data members can vary independently.

Readability. Ease of comprehension. The use of class alerts the programmer to the need for an invariant. This is a useful convention.

**Note**
> An invariant is a logical condition for the members of an object that a constructor must establish for the public member functions to assume. 
> After the invariant is established (typically by a constructor) every member function can be called for the object. An invariant can be stated informally (e.g., in a comment) or more formally using Expects.
>
> If all data members can vary independently of each other, no invariant is possible.

### Example
```cpp
struct Pair {  // the members can vary independently
    string name;
    int volume;
};
```
but:
```cpp
class Date {
public:
    // validate that {yy, mm, dd} is a valid date and initialize
    Date(int yy, Month mm, char dd);
    // ...
private:
    int y;
    Month m;
    char d;    // day
};
```

## Avoid protected data
Protected data is a source of complexity and errors. protected data complicated the statement of invariants. 
protected data inherently violates the guidance against putting data in base classes, which usually leads to having to deal virtual inheritance as well.

Protected member function can be just fine.

## Use class hierarchies to represent concepts with inherent hierarchical structure (only)
Direct representation of ideas in code eases comprehension and maintenance. Make sure the idea represented in the base class exactly matches all derived types and there is not a better way to express it than using the tight coupling of inheritance.
Do not use inheritance when simply having a data member will do. Usually this means that the derived type needs to override a base virtual function or needs access to a protected member.

### Example
 ... can be an example with a class that inherits from the base class and from ISomeListener...

## Ordering
TBD
    - methods
    - members

## Declarations
TBD
    - alignment
    - members

## Templates
TBD

