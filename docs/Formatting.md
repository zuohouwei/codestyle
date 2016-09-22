[Main Page](README.md)

# Table of contents
* [Indentation](#Indentation)
* [Braces](#Braces)
* [Whitespace](#Whitespace)
* [Line Wraping](#Line Wraping)
* [Control Statements](#Control Statements)
* [Comments](#Comments)

## Indentation
## Braces
## Whitespace
### Tabs vs. Spaces
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

### Trailing whitespaces
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

### Rational
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
else {/*default case*/}

</pre></td></tr>
</table>

### For-Loops
Curly brackets go into new lines.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

for (int i = 1; i < 20; ++i)
{
    //do something
}

</pre></td><td><pre lang="cpp">

for (int i = 1; i < 20; ++i) {
    //do something
}

</pre></td></tr>
</table>

### While-Loops
Curly brackets go into new lines, except the do while loop.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

while (condition)
{
    //do something
}

do {
    //something
} while (condition);

</pre></td><td><pre lang="cpp">

while (condition) {
    //do something
}

do
{
    //something
} while (condition);


</pre></td></tr>
</table>

### Switch-Case

Curly brackets go into new lines. Every switch statement must have a default branch.

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

switch (var)
{
    case 1:
        //code for case 1
        break;
    case 2:
        //code for case 2
        break;
    default:
        //default code
        break;
}

</pre></td><td><pre lang="cpp">

switch (var) {
case 1:
    //code for case 1
    break;
case 2:
    //code for case 2
    break;
}

</pre></td></tr>
</table>

## Comments
