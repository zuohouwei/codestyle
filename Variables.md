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
:white_check_mark: Variable names are camelCase

:white_check_mark: Boolean variables start with _is_ or _has_

:white_check_mark: Member variables are prefixed with *f*, *m* or *_*
