# E.S.R.Labs C++ Code Style
Code style is a matter of personal taste and discussions about it tend to become emotional. In order to prevent religious wars, we define an E.S.R.Labs set of style rules.

##### Table of Contents  
* [Tabs vs. Spaces](#tabs-vs-spaces)
* [Class Names](#class-names)  
* [Function Names](#function-names)  
* [Variable Names](#variable-names)  
* [Constants](#constants)


# Tabs vs. Spaces
All of our code should be **tab-free**! For *indentation* use **4 spaces.**

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class Listener
:   ::esrlabs::estd::forward_list_node<Listener>
{
public:
    void doWork();
};

</pre></td><td><pre lang="cpp">

class Listener
: ::esrlabs::estd::forward_list_node<Listener>
{
public:
  void doWork();
};

</pre></td></tr>
</table>

## Summary
:+1: Indentation 4 spaces

:-1: Tabs


# Class Names
Class names are written in camel case starting with a capital letter. Also abbreviations like CAN are camel case: Can. _Interface names_ start prefixed with a capital **I**. Names of abstract classes are not treated specially any more, we used to prefix them with **Abstract**.

In unit tests, when writing a mock, the class name is usually postfixed with **Mock**.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class CanTransceiver;
class CanTransceiverMock;
class FilteredLinFrameListerner;
class ITransportMessageProvider; //interface

</pre></td><td><pre lang="cpp">

class CANTransceiver;
class filteredLINFrameListener;
class AbstractDiagJob; //should be DiagJob

</pre></td></tr>
</table>

## Summary
:+1: Class names are CamelCase


# Function Names
Function names are written in camelCase starting with a lower case letter.

Try to be precise without repeating yourself. For example if you provide a
function to send a `CanFrame` just call it `send` instead of `sendCanFrame`.
The signature tells the user that this function sends a `CanFrame`.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void shutdownEcu();

class CanTransceiver
{
public:
    ErrorCode send(const CanFrame& frame);

    static bool addGlobalListener(
        ICanFrameListener& listener);
};

</pre></td><td><pre lang="cpp">

void ShutdownEcu();

class CanTransceiver
{
public:
    ErrorCode SendFrame(const CanFrame& frame);

    static bool AddGlobalListener(
        ICanFrameListener& listener);
};

</pre></td></tr>
</table>

## Boolean Functions
If a function returns a boolean value which is not intended to signal success
or failure of the function call, the function should start with _is_ or _has_.
Boolean member functions tend to be `const`.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

bool isEcuInSleepMode();

class CanTransceiver
{
public:
    bool hasWakeupOccurred() const;
};

</pre></td><td><pre lang="cpp">

bool sleepModeActive();

class CanTransceiver
{
public:
    bool wakeupOccurred();
};

</pre></td></tr>
</table>

## Getters, Setters, Attribute Functions
In general `set` functions should be avoided. Classes should be initialized
when calling their constructor. To read properties of a class, avoid `get`
functions, instead use `const` attribute style functions.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class CanTransceiver
{
public:
    CanTransceiver(BusId id);

    BusId busId() const;
};

</pre></td><td><pre lang="cpp">

class CanTransceiver
{
public:
    void setBusId(BusId id);

    BusId getBusId() const;
};

</pre></td></tr>
</table>

## Summary
:+1: Function names are camelCase

:+1: Boolean functions start with _is_ or _has_

:+1: Consider signature part of name

:+1: Getters should use attribute style

# Variable Names
Variable names are written in camelCase starting with a lower case letter.

We do *not* use [Hungarian Notation](https://en.wikipedia.org/wiki/Hungarian_notation),
although you sometimes might find the prefix **p** for pointers or **s** for
static member variables.

All variable names like global variable names, local variable name, function
parameter names are treated similarly. The exception are member variable
names.

In general, spend time finding good variable names. Don't try to abbreviate
too much, also don't use patterns like stripping vowels from names to make
them shorter. Also `a`, `b` or `z` are normally not good choices ;-).

Reading your code should be pleasant and joyful to others.

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
<tr><td><pre lang="cpp">

class CanTransceiver
{
    ::estd::forward_list<ICanFrameListener> fListeners;
};

struct Result
{
    ::bsp::ErrorCode status;
    uint16_t value;
};

</pre></td><td><pre lang="cpp">

class CanTransceiver
{
    ::estd::forward_list<ICanFrameListener> listeners;
};

struct Result
{
    ::bsp::ErrorCode Status;
    uint16_t value_;
};

</pre></td></tr>
</table>

## Global, Local, Parameter Names

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode mode,
    ::lifecycle::Manager* pManager)
{
    ::lifecycle::Manager::TransitionResult result =
        ::lifecycle::Manager::TransitionResult::NONE;
}

</pre></td><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode Md,
    ::lifecycle::Manager* ptr_mgr)
{
    ::lifecycle::Manager::TransitionResult r =
        ::lifecycle::Manager::TransitionResult::NONE;
}
</pre></td></tr>
</table>

## Boolean Variables
Boolean variables should start with _is_ or _has_.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void shutdown(Connection& connection)
{
    bool isSuccessfullyTerminated =
        connection.terminate();
}

</pre></td><td><pre lang="cpp">

void shutdown(Connection& connection)
{
    bool terminated = connection.terminate();
}

</pre></td></tr>
</table>

## Summary
:+1: Variable names are camelCase

:+1: Boolean variables start with _is_ or _has_

:+1: Member variables are prefixed with *f*, *m* or *_*

# Constants
Constants including `enum` values are written all UPPER_CASE with underscore
word separation.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

enum PhyAddress
{
    PHY_0,
    PHY_1    
};

class CanTransceiver
{
public:
    static const
    uint32_t BAUDRATE_HIGH_SPEED = 500000U;    
};

</pre></td><td><pre lang="cpp">

enum PhyAddress
{
    phy0,
    phy1    
};

class CanTransceiver
{
public:
    static const
    uint32_t BaudrateHighSpeed = 500000U;    
};

</pre></td></tr>
</table>

## Summary
:+1: Constants are all UPPER_CASE


# File Names
Files that contain classes should contain only one class. The header and
source file are named like the class **MyClass.h** and **MyClass,cpp**.
The extension for C++ source files is *.cpp*, the extension for C source files
is *.c*, the extension for assembly files is *.s*. Header files have the
extension *.h* no matter which content. Sometimes you might find *.hpp* files
that contain implementation source code of class templates.

# Include Guards
Include guards shall prevent code from being processed multiple times which
would cause compilation errors. There are two forms of allowed include guards:
1. All capital letter path beginning after the *include* folder separated by  
   underscore and terminated by *_H_*.
2. A unique identifier like *HE793FCD8_FC04_45D3_A438_533341BBA7B1*

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td>
```cpp
//File: include/can/CanTransceiver.h

#ifndef CAN_CANTRANSCEIVER_H_
#define CAN_CANTRANSCEIVER_H_

#endif /* CAN_CANTRANSCEIVER_H_ */

//File: include/bsp/ethernet/Bcm89811.h

#ifndef HE793FCD8_FC04_45D3_A438_533341BBA7B1
#define HE793FCD8_FC04_45D3_A438_533341BBA7B1

#endif /* HE793FCD8_FC04_45D3_A438_533341BBA7B1 */
```
</td><td>
```cpp
//File: include/can/CanTransceiver.h

#ifndef CANTRANSCEIVER_H_
#define CANTRANSCEIVER_H_

#endif /* CANTRANSCEIVER_H_ */

//File: include/bsp/ethernet/Bcm89811.h

#ifndef HE793FCD8_FC04_45D3_A438_533341BBA7B1
#define HE793FCD8_FC04_45D3_A438_533341BBA7B1

#endif
```
</td></tr>
</table>

## Summary
:+1: Include guard is all UPPER_CASE file name + path
:+1: Include guard is unique identifier
