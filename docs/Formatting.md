# Indentation
# Braces
# Whitespace (Tabs Vs. Space)
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

### Example
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

# Line Wraping

# Control Statements

# Comments
