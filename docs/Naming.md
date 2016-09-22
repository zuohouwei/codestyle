# Content
[Class-naming](#class)


## Abreviation Names
Abreviation shold be written in lower-case with the capital first letter
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
Function names are written in 'camelCase' starting with a lower case letter.
Function name should be a verb, it should refleck an action.

Try to be precise without repeating yourself. For example if you provide a
function to send a `CanFrame` just call it `send` instead of `sendCanFrame`.
The signature tells the user that this function sends a `CanFrame`.

### Example
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

## #Boolean Functions
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

## Variable Names
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

### Boolean Variables
Boolean variables should start with 'is' or 'has'.

#### Example
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
:white_check_mark: Variable names are camelCase

:white_check_mark: Boolean variables start with _is_ or _has_

:white_check_mark: Member variables are prefixed with *f*, *m* or *_*

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

## Constants
All the constants should be upper_case
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

const uint32_t INITIAL_TIME = 1;

</pre></td><td><pre lang="cpp">

const uint32_t cInitialTime = 1;

</pre></td></tr>
</table>


## Type Names
Type names, such as typedef, struct, union, class should
be written in 'CamelCase'
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

# Class

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


