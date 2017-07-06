# Table of contents
* [#Single Responsibility Principle & Separation of Concerns](#Single Responsibility Principle & Separation of Concerns)

# Single Responsibility Principle & Separation of Concerns
Every class should have only a single responsibility and the
class should be concerned only about a single aspect of that responsibility.
That means: Rather have smaller, more focussed classes than a
single master-I-can-do-everything class.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">


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


</pre></td><td><pre lang="cpp">

public class CarDoor {
    public void openWindow() { }
    public void closeWindow() { }
    public void openDoor() { }
    public void turnOnLights() { }
    public void turnOffLights() { }
}

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