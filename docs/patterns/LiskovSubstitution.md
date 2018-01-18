[Patterns](../Patterns.md)

# The Liskov Substitution Principle

The **L**iskov **S**ubstitution **P**rinciple (**LSP**) states that in a well designed system, functions receiving pointers or references to base classes must be able to use objects of derived classes without knowing it. 

## Example:

<table>
<tr><th width="400px">Better</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
void DrawShape(const Shape& s) {
  s.DrawYourself();
}
void Square::DrawYourself() {
  DrawSquare(*this);
}
```
</pre></td><td><pre lang="cpp">

```cpp
void DrawShape(const Shape& s) {
  if (typeid(s) == typeid(Square))
    DrawSquare(static_cast<Square&>(s));
  else if (typeid(s) == typeid(Circle))
    DrawCircle(static_cast<Circle&>(s));
  // Only circle and square are supported
}
```

</pre></td></tr>
</table>

In the bad example, if we add a new shape, we need to modify the DrawShape function. In the better example the DrawShape function can receive objects of derived classes without knowing it.
It can even receive objects of classes that didn’t exist at the time of its writing. This is very powerful, code that is open to change and closed to modification. 

In dynamic languages, this principle is even more important. Because of the lack of a type checker, methods can receive objects of unrelated types, so the need to check if an object is of a certain type is greater.
Through better design (appropriate interfaces), functions can remain agnostic of actual types. Another option, is to check if an object has the method needed. In Ruby this is possible with the “respond_to?” method.

The **LSP** is more than just avoiding type identification. According to Bertrand Meyer:
“**...when redefining a routine [in a derivative], you may only replace its precondition by a weaker one, and its postcondition by a stronger one**”.
Under this new rule, a Square class deriving from a Rectangle class would not be possible, since setting the width of a square would change the height as well,
thus breaking the postcondition that the width setter changes nothing else in a Rectangle object. Clients could be surprised by this. 

Overriding methods should only return types derived from the return type of the base method. They should also not throw new exceptions.
The new method should throw only exceptions of the same type or derived types as the base method. This is all about making clients agnostic of the diversity of objects passed in as parameters.

