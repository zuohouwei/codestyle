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
:white_check_mark: Class names are CamelCase

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
:white_check_mark: Function names are camelCase

:white_check_mark: Boolean functions start with _is_ or _has_

:white_check_mark: Consider signature part of name

:white_check_mark: Getters should use attribute style

