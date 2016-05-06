# E.S.R.Labs C++ Code Style
Code style is a matter of personal taste and discussions about it tend to become emotional. In order to prevent religious wars, we define an E.S.R.Labs set of style rules.

## Tabs vs. Spaces
All of our code should be **tab-free**! For *indentation* use **4 spaces.**

### Summary
:+1: Indentation 4 spaces

:-1: Tabs

### Example

<table>
<tr><th width="30%">Good</th><th width="30%">Bad</th></tr>
<tr>
<td>
<pre lang="cpp">
class Listener
:   ::esrlabs::estd::forward_list_node<Listener>
{
public:
    void doWork();
};
</pre>
</td>
<td>
<pre lang="cpp">
class Listener
: ::esrlabs::estd::forward_list_node<Listener>
{
public:
  void doWork();
};
</pre>
</td>
</tr>
</table>

### Example, Good
```cpp
class Listener
:   ::esrlabs::estd::forward_list_node<Listener>
{
public:
    void doWork();
};
```

### Example, Bad
```cpp
class Listener
: ::esrlabs::estd::forward_list_node<Listener>
{
public:
  void doWork();
};
```
