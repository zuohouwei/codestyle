[Patterns](../Patterns.md)

# The single responsibility principle

This is the first episode of the series on the SOLID Object Oriented Design principles promoted by Uncle Bob (Robert C. Martin). 
The **SOLID** **O**bject **O**riented **D**esign principles are:
- **S**ingle Responsibility Principle (SRP), 
- **O**pen Closed Principle (OCP), 
- **L**iskov Substitution Principle (LSP), 
- **I**nterface Segregation Principle (ISP)
- **D**ependency Inversion Principle, (DIP)
The first principle (SRP) states that a class should have a single responsibility or a single reason to change. Because inside a class there is no encapsulation, the different responsibilities become coupled together and they have to change together. Violations of SRP lead to classes that need to change more often and which are more difficult to change when requirements change.

## Example:

<table>
<tr><th width="400px">Better</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
class Rectangle {
  public:
    float getArea();
    float getCircumference();
};
...
#include <GraphicsLibrary.h>
class Graphics {
  public:
    void draw(GUI &ctx, Rectangle r);
    void clearArea(GUI &ctx, Rectangle r);
};
```
</pre></td><td><pre lang="cpp">

```cpp
#include <GraphicsLibrary.h>
class Rectangle {
  public:
    void draw(GUI &ctx);
    void clearArea(GUI &ctx);
    float getArea();
    float getCircumference();
};
```

</pre></td></tr>
</table>


In the bad example the Rectangle class has 2 responsibilities: mathematical calculations and graphics. Violations of SRP lead to unnecessary dependencies, clients wanting to compute area depend also on the graphics library. 

Caution: If two responsibilities are unlikely to change during the lifetime of the product, it is unwise to separate them. The excessive application of SRP leads to needless complexity.
