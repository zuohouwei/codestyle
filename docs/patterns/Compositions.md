[Patterns](../Patterns.md)

# Favor composition over inheritance
Software architecture should prefer classes that are composed out of various other classes than classes which have a deep type inheritance structure.
As soon as classes have about >= 3 layers of inheritance, it becomes difficult to adjust any layer because they are strongly coupled to each other.

## Example with only 2 layers
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
interface CarDoor {
  public void open();
}

class ActualCarDoor implements CarDoor {
  public void open() { /*actually open*/ }
}

class SecurityCarDoor implements CarDoor {
  private CarDoor actualCarDoor;

  public void open() {
    closeWindowIfNeeded();
    actualCarDoor.open();
  }
}
```
</pre></td><td><pre lang="cpp">

```cpp
class CarDoor {
  protected List<Action> openActions;


  public void open() {
    openActions.forEach(a -> a.execute());
  }
}

class SecurityCarDoor extends CarDoor {
  @Override
  public void open() {
    if (!openActionsHasCloseWindow()) {
      openActions.add(new CloseWindow());
    }
    super.open();
  }
}
```

</pre></td></tr>
</table>

In this example, there is a strong dependency of the subclass `SecurityCarDoor` on how the parent class `CarDoor` works internally.
It is obvious that e.g. CarDoor is harder to adjust. Imagine a case where we have more layers and more classes… 

You could also think of the above solution as adhering to the SRP (principle “open” is different from “security”, see episode 1).
Note that *favoring* composition does not mean that you should *never* use inheritance. Find a meaningful solution together!

## Why?
Again: Easier to *understand*, easier to *adjust*, easier to *test* (mock CarDoor!). 
Additionally, the code gets more *flexible*, since we can e.g. apply a *Decorator* pattern more easily (as we did in the example, `SecurityCarDoor`
is a Decorator).
