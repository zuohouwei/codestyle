[Main Page](../README.md)

# Table of contents
* [Single Responsibility Principle and Separation of Concerns](#single_responsibility_principle_and_separation_of_concerns)
* [Favor composition over inheritance](#favor_composition_over_inheritance)

# Single Responsibility Principle and Separation of Concerns

Every class should have only a single responsibility and the
class should be concerned only about a single aspect of that responsibility.
That means: Rather have smaller, more focussed classes than a
single master-I-can-do-everything class.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
public class CarDoor {
    public void open() { }
}


public class WindowRegulator {
    public void open() { }
    public void close() { }
}

public class CarDoorLights {
    public void turnOn() { }
    public void turnOff() { }
}
```
</pre></td><td><pre lang="cpp">

```cpp
public class CarDoor {
    public void openWindow() { }
    public void closeWindow() { }
    public void openDoor() { }
    public void turnOnLights() { }
    public void turnOffLights() { }
}
```

</pre></td></tr>
</table>

## Responsibility vs. Concern
In this context they mean similar things: “Responsibility” stands rather for a
*functionally different* entity (e.g. CarDoorLights vs. WindowRegulator),
“Concern” is more *what the class does* with the entity (load/store, act on the entity itself etc.)
 -  all of these might be different classes!

## Watch out!
Be careful to make the classes *not too small*, but find a meaningful level of separation.
Speak to other engineers and/or do code reviews to identify how to split your classes well!

## Why?
Easier to *understand*, easier to *adjust*, easier to *test*.

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

##Why?
Again: Easier to *understand*, easier to *adjust*, easier to *test* (mock CarDoor!). 
Additionally, the code gets more *flexible*, since we can e.g. apply a *Decorator* pattern more easily (as we did in the example, `SecurityCarDoor` is a Decorator).
