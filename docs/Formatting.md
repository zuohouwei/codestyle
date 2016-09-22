[Main Page](README.md)

# Table of contents
* [Indentation](#Indentation)
* [Braces](#Braces)
* [Whitespace (Tabs Vs. Space)](#Whitespace (Tabs Vs. Space))
* [Line Wraping](#Line Wraping)
* [Control Statements](#Control Statements)
* [Comments](#Comments)

## Indentation
## Braces
## Whitespace (Tabs Vs. Space)
## Tabs vs. Spaces
All of our code should be **tab-free**! For *indentation* use **4 spaces.**

### Example
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

### Summary
:white_check_mark: Indentation 4 spaces

:no_entry: Tabs

## Trailing whitespaces
There must not be any trailing whitespace. It is highly recommended to adjust your IDE to highlight trailing whitespaces.

## Line breaks
If a list of parameters to a function becomes to long to fit into one line, each parameter goes into a separate line.

### Examples
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void MyClass::functionWithManyParams(
    int parameter1,
    int parameter2,
    int parameter3,
    int parameter4
);

</pre></td><td><pre lang="cpp">

void MyClass::functionWithManyParams(int parameter1, int parameter2, int parameter3, int parameter4);

</pre></td></tr>
</table>

<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

PortSync::sendAnnounceMessage()
{
    fAnnounceMessage.setSequenceId(fAnnounceSequenceId);
    fAnnounceMessage.setLogMessageInterval(fAnnounceLogMessageInterval);
    fRawEthernetSend(
            slice<uint8_t>::from_pointer(
                &(fAnnounceBuffer[0]),
                PtpMessage::PTP_ANNOUNCE_MESSAGE_LENGTH
            ),
            DataSentCallback()
    );
    ++fAnnounceSequenceId;
}

</pre></td><td><pre lang="cpp">

PortSync::sendAnnounceMessage()
{
    fAnnounceMessage.setSequenceId(fAnnounceSequenceId);
    fAnnounceMessage.setLogMessageInterval(fAnnounceLogMessageInterval);
    fRawEthernetSend(slice<uint8_t>::from_pointer(&(fAnnounceBuffer[0]), PtpMessage::PTP_ANNOUNCE_MESSAGE_LENGTH), DataSentCallback());
    ++fAnnounceSequenceId;
}

</pre></td></tr>
</table>

## Line Wraping
Each line of text in your code should be at most 120 characters long.

### Logic
At most 80 characters was used by old retarded people.

## Control Statements

### If-statements
Curly brackets go into new lines.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

if (condition)
{
    //do something
}
else if (condition2)
{
    //do something else
}
else
{
    //default case
}

</pre></td><td><pre lang="cpp">

if (condition) {
    //do something
}
else if (condition2)
    //do something else
else {//default case}

</pre></td></tr>
</table>

## Comments
