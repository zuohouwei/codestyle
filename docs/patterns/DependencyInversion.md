[Patterns](../Patterns.md)

# The Dependency Inversion Principle
Interdependence of modules results in bad designs.

Bad design is one that is hard to change (Rigidity), which breaks easily when changed (Fragility), and hard to use in another application (Immobility).
The interdependence of modules makes design rigid, fragile and immobile. A single change in one module cascades into changes to other modules.
Impact is hard to estimate and costs skyrocket.

Traditionally high-level modules depend on low-level modules. We call this a hierarchical structure. Imagine a simple program where a button turns on
and off a Lamp. The button class will depend on the *Lamp* class.

Example:

![alt text](https://github.com/esrlabs/codestyle/blob/master/docs/patterns/DependencyInversion.png "Example Dependency Inversion")

In the good example dependencies are inverted, both Button and Lamp depend on abstract interfaces and can function with new classes. Dependency arrows
point up. A physical button can be changed to a software button and the Lamp can be changed to a Motor. As long as classes talk to abstract interfaces,
objects are interchangeable.

Dependency Inversion Principle Rules:
* High level modules should not depend upon low level modules. Both should depend upon abstractions.
* Abstractions should not depend upon details. Details should depend upon abstractions. 

Another example of dependency inversion is the IO system in an operating system. A software program can open a file or a socket and uses the same functions
(read/write) to write bytes to disk or to send them over the internet. The interface remains the same and the file descriptors are not distinguishable from socket descriptors.

