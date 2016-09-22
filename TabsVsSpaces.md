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
:white_check_mark: Indentation 4 spaces

:no_entry: Tabs



