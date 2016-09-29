[Main Page](../README.md)

# Table of contents
* [Library Support](#library_support)

## Library Support
[P.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#p3-express-intent) A programmer should be familiar with

* [The guideline support library](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#S-gsl)
* [The ISO C++ standard library](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#S-stdlib)
* Whatever foundation libraries are used for the current project(s)

## Prefer compile-time checking to run-time checking
### Use estd::slice
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void read(estd::slice<int> buffer);

int a[100];
read(a);
</pre></td><td><pre lang="cpp">

void read(int* pBuffer, size_t buffSize);

int a[100];
read(a, 1000);
</pre></td></tr>
</table>
Don't postpone to run time what can be done well at compile time.

