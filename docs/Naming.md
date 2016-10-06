[Main Page](../README.md)

# Table of contents
* [Abbreviation Names](#abbreviation-names)
* [Function Names](#function-names)
* [Boolean Functions](#boolean-functions)
* [Global, Local, Parameter Names](#global-local-parameter-names)
* [Types](#type-names)
* [Constants](#constants)
* [Variable Names](#variable-names)
* [Class-naming](#class)
* [Private members](#private-members)

## All names should be in English
Only if there is a necessity to use names from a documentation in
original Language, then it's allowed, otherwise, please, use English.

## Abbreviation Names
Abbreviation should be written in lower-case with the capital first letter
When the name is connected to another, the readability is seriously reduced; the word following the abbreviation does not stand out as it should.
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

exportHtmlSource();

initUsbDevice();

</pre></td><td><pre lang="cpp">

exportHTMLSource();

initUSBDevice();

</pre></td></tr>
</table>


## Function Names
Names representing functions must be verbs and written in mixed case starting with lower case.

The name of the object is implicit, and should be avoided in a method name.
Try to be precise without repeating yourself. For example if you provide a
function to send a `CanFrame` just call it `send` instead of `sendCanFrame`.
The signature tells the user that this function sends a `CanFrame`.
```cpp

```

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

line.getLength();

</pre></td><td><pre lang="cpp">

void ShutdownEcu();

class CanTransceiver
{
public:
    ErrorCode SendFrame(const CanFrame& frame);

    static bool AddGlobalListener(
        ICanFrameListener& listener);
};

line.getLineLength();

</pre></td></tr>
</table>


## Boolean Functions
If a function returns a boolean value which is not intended to signal success
or failure of the function call, the function should start with _is_ or _has_.
Boolean member functions tend to be `const`.

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

# Global, Local, Parameter Names

* All the variables should be readable and make sense.
* If it's possible to not create new abbreviation, then don't.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

Manager::TransitionResult
connect(
    Database database,
    Manager* manager
)
{
    database.add(manager);
    Manager::TransitionResult result =
        Manager::TransitionResult::NONE;
    return result;
}

</pre></td><td><pre lang="cpp">

Manager::TransitionResult
connect(
    Database db,
    Manager* mgr
)
{
    db.add(mgr);
    Manager::TransitionResult rst =
        Manager::TransitionResult::NONE;
    return rst;
}

</pre></td></tr>
</table>

## Type Names
Names representing types must be in mixed case starting with upper case.

<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

template <size_t PAYLOAD_SIZE>
class CanFrame
{
    ...
}

typedef CanFrame<64> CanFdFrame;

</pre></td><td><pre lang="cpp">

template <size_t PAYLOAD_SIZE>
class CANFrame
{
    ...
}

typedef CANFrame<64> CANFdFrame;
</pre></td></tr>
</table>

## Constants
Named constants (including enumeration values) must be all uppercase using underscore to separate words.
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

const uint32_t INITIAL_TIME = 1;

</pre></td><td><pre lang="cpp">

const uint32_t cInitialTime = 1;

</pre></td></tr>
</table>

## Variable Names
Variable names must be in mixed case starting with lower case.

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

### Boolean Variables
Boolean variables should start with 'is' or 'has'.

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

### Plural form should be used on names representing a collection of objects.
Enhances readability since the name gives the user an immediate clue of the type
of the variable and the operations that can be performed on its elements.

```cpp
vector<Point>  points;
int            values[];
```

### Negated boolean variable names must be avoided
The problem arises when such a name is used in conjunction with the logical negation operator as this results in a double negative. It is not immediately apparent what !isNotFound means.

<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

bool isError;
bool isFound;

</pre></td><td><pre lang="cpp">

bool isNoError
bool isNotFound

</pre></td></tr>
</table>

## Summary
:white_check_mark: Variable names are camelCase

:white_check_mark: Boolean variables start with _is_ or _has_

:white_check_mark: Member variables are prefixed with the underscore *_*

## Namespaces
Names representing namespaces should be all lowercase.
`model::analyzer, io::iomanager, common::math::geometry`

# Class
## Public Methods
Names representing methods must be verbs and written in mixed case starting with lower case.

## Private Members
Should be with underscore prefix
Private members are important to keep in mind and to distignuish from local variables,
so underscore prefix make it possible to see it better and to operate more carefully
with them.

<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

class Box
{
public:

	Box(int depth)
	: _depth(depth)
	{ }

private:

	int _depth;
}
</pre></td><td><pre lang="cpp">

class Box
{
public:

	Box(int depth)
	: fDepth(depth)
	{ }

private:

	int fDepth;
}

</pre></td></tr>
</table>

:warning:

> From the 2003 C++ Standard:

> 17.4.3.1.2 Global names [lib.global.names]

> Certain sets of names and function signatures are always reserved to the implementation:

> * Each name that contains a double underscore (_ _) or begins with an underscore followed by an uppercase letter (2.11) is reserved to the implementation for any use.

> * Each name that begins with an underscore is reserved to the implementation for use as a name in the global namespace.
> Such names are also reserved in namespace ::std (17.4.3.1).


