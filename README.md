# E.S.R.Labs C++ Code Style
Code style is a matter of personal taste and discussions about it tend to become emotional. In order to prevent religious wars, we define an E.S.R.Labs set of style rules.

##### Table of Contents  
* [Tabs vs. Spaces](#tabs-vs-spaces)
* [Class Names](#class-names)  
* [Function Names](#function-names)  


# Tabs vs. Spaces
All of our code should be **tab-free**! For *indentation* use **4 spaces.**

## Summary
:+1: Indentation 4 spaces

:-1: Tabs

## Example
<table>
<tr><th width="33%">Good</th><th width="33%">Bad</th></tr>
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


# Class names
Class names are written in camel case starting with a capital letter. Also abbreviations like CAN are camel case: Can. _Interface names_ start prefixed with a capital **I**. Names of abstract classes are not treated specially any more, we used to prefix them with **Abstract**.

In unit tests, when writing a mock, the class name is usually postfixed with **Mock**.

## Summary
:+1: Class names are CamelCase

## Example
<table>
<tr><th width="33%">Good</th><th width="33%">Bad</th></tr>
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


# Function names
Function names are written in camel case starting with a lower case letter.

Try to be precise without repeating yourself. For example if you provide a
function to send a `CanFrame` just call it `send` instead of `sendCanFrame`.
The signature tells the user that this function sends a `CanFrame`.


## Summary
:+1: Function names are camelCase

:+1: Consider signature part of name

## Example
<table>
<tr><th width="33%">Good</th><th width="33%">Bad</th></tr>
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
