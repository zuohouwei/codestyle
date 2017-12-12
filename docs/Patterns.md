[Main Page](../README.md)

# Table of contents
* [Single Responsibility Principle and Separation of Concerns](Patterns.md#single-responsibility-principle-and-separation-of-concerns)
* [Favor composition over inheritance](Patterns.md#favor-composition-over-inheritance)
* [Automated tests, tests, tests](Patterns.md#automated-tests-tests-tests)
* [Minimize public member dependencies](Patterns.md#minimize-public-member-dependencies)
* [Dependency Injection (1)](Patterns.md#dependency-injection-1)
* [Dependency Injection (2)](Patterns.md#dependency-injection-2)
* [The single responsibility principle](patterns/Responsibility.md)
* [The Open Closed principle](patterns/OpenClosed.md)

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

## Why?
Again: Easier to *understand*, easier to *adjust*, easier to *test* (mock CarDoor!). 
Additionally, the code gets more *flexible*, since we can e.g. apply a *Decorator* pattern more easily (as we did in the example, `SecurityCarDoor`
is a Decorator).


# Automated tests, tests, tests
All developed software must be enriched by fully automated tests. This is crucial for ensuring that we provide high-quality
software over the full lifetime of a project! In general, the earlier a bug is found, the less overhead it is to fix it and
the fewer money it costs therefore. Releases are not stressful anymore!

**Automated tests** are executed automatically on a regular basis (preferably before/after each commit; or nightly)
by Continuous Integration (http://jenkins/).

**Manual tests** are tests which are (setup and) executed manually on demand.
There should be no manual tests required for any project (with a few exceptions, though IMHO none of those are matching projects at E.S.R.Labs).

## Why automated?

- Software in the repository is in releasable state always
- Return test results quickly
- Fully reproducible test results
- Required for volatile teams (people joining/leaving)
- test-fix-test-fix-test-fix-...
- Correctness of features the engineer does not know about
- Easily test against multiple versions of another software

## Notes

- It is fine (and even likely) to: Lines of test code > Lines of productive code
- You can also formulate **organizational constraints** as tests as well (e.g. an external company implements code using a specific version of your interface)
- Every component without enough good tests has considerable **technical debt**
- Every project must have a **test framework** that enables every engineer to write every kind of test without any hassle
- There are **unit and integration tests**, talk to each other to find out how your project separates them and how your team implements tests with **real HW**
- Can and should also be implemented for integrating code of **various teams**

## Handling failing tests
If any test fails, this has to be fixed immediately, favourably by the one who broke it. It is high(est) priority of the team to keep the test CI job green. Otherwise no one else in the team can reliably continue to work or will receive test errors late.

# Minimize public member dependencies
The number of public members of classes should be minimal. Public members for interfaces should be grouped reasonably and each group should be minimal.
Each public member creates a logical dependency from the one referencing an object to the one providing it. It is obvious that the smaller the amount of dependencies between components, the easier it is to change (and improve) code. 
Each component should reference only objects of such types that provide a reasonable superset of methods required by that component.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
interface Shutdownable {
  public void shutdown();
}

class VoiceCall implements Shutdownable {
  ButtonPressListener pressListener = ..;   
  public void dial(String number) { }
  @Override    
  public void shutdown() { }
}

class ShutdownManager {
  private List<Shutdownable> shutdown=..;
  public void executeEcuShutdown() {
    shutdownables.forEach(/* .... */);
  }
}
```
</pre></td><td><pre lang="cpp">

```cpp
class VoiceCall
  implements ButtonPressListener {

  @Override
  public void onButtonPress(){/*hangup*/}
   
  public void dial(String number) { }
  public void shutdown() { }
}

class ShutdownManager {
    private VoiceCall voiceCall;
   
    public void executeEcuShutdown() {
        voiceCall.shutdown();
    }
}
```

</pre></td></tr>
</table>

In the bad example, `VoiceCall` itself implements `ButtonPressListener`, thereby publishing the `onButtonPress` method to everyone else,
though no one will actually need it - make it a private class instead! In addition to that, the `ShutdownManager` on the left depends on
the whole `VoiceCall`, which means that someone changing `VoiceCall` will actually need to inspect the manager class and changing the manager
class might require thinking about which methods to call of `VoiceCall`. It is better to create a interface that has a meaningfully grouped set
of methods (in this simple case: only shutdown) and depend on that only in the manager.

The Interface Segregation Principle takes this even one step further! Though: stay reasonable always ;-)

# Dependency Injection (1)
A component should not create objects it depends on by itself, but these should be provided from the outside.
Providing the objects can be done using constructor parameters (typically at least for required dependencies) or setter methods (possibly for
optional ones).

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
class ServiceAImpl implements ServiceA {
  public ServiceAImpl(ServiceB b) {
    serviceB = b;
  }
   
  // or (setter injection):
  public ServiceAImpl() { }
  public void setServiceB(ServiceB b) {
    serviceB = b;
  }
}

interface ServiceB { /* ... */ }
```
</pre></td><td><pre lang="cpp">

```cpp
class ServiceA {
  private ServiceB serviceB;
  public ServiceA() {
    serviceB = new ServiceB();
  }
   
  // or (static lookup):
  public ServiceA() {
    serviceB = StaticAccess.findServiceB();
  }
}

class ServiceB{ /* ... */ }
```

</pre></td></tr>
</table>

By using methods like displayed on the left side (instantiate yourself, find by some static provider, ...),
`ServiceA` is easily coupled to class `ServiceB` too tightly. In the approach on the right side, each Service is an interface and `ServiceAImpl`
depends only on the generic interface of `ServiceB`, not on a concrete implementation. This allows easy substitution of the implementation -
think e.g. of a Service that needs to persistently store some byte array; it should not care if a StorageService stores on local disk, remote disk,
or only in main memory for tests. In addition the dependency of `ServiceAImpl` to some `ServiceB` is directly visible (at least for the constructor
injection).

Some classes obviously have to instantiate objects though, for example data objects after reading them e.g. from disk. These objects should though
only be created by Factory classes, which again have an interface and are injected.
The classes which need injection should be instantiated favorably in a single place, with that single component resolving all the dependencies and
creating the objects in the right order.

# Dependency Injection (2)
There must only be a single source of truth.

Example: Assume there’s a constant-to-int mapping that needs to be shared between two modules or even between C++ and Java source:
Create a single file specifying the mapping and generate code for both parts out of it!

## Dependency Injection Example
Assume `ServiceAImpl` depends on ServiceB:

<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
class DiContainer {
  public void bootstrap() { // pseudo code
    impls = [ ServiceA -> ServiceAImpl
              ServiceB -> ServiceBImpl ]
    deps = findDependencies(impls);
    correctOrder = topologicalSort(deps);
    for (cls : correctOrder) {
      instantiate(cls);
    }
  }
}
```
</pre></td><td><pre lang="cpp">

```cpp
class DiContainer {
  public void bootstrap() {
    // manual instantiation
    ServiceB b = new ServiceBImpl();
    ServiceA a = new ServiceAImpl(b);
  }
}
```

</pre></td></tr>
</table>

The Dependency Injection Container on the left is unclean if it is written by hand, although this looks like less code in this small example
(imagine having hundreds of services; every developer has to know the order; there is high risk that a service implementation relies on a
concrete order, creating “invisible” dependencies; ...).

On the right side, we use a mapping from interface to actual class as input, calculate the dependencies of each of those on demand
i.e. by inspecting the constructor parameters) and execute a topological sort (see Wikipedia) on the resulting graph. We can then iterate
over an ordered list of services where all dependencies are guaranteed to be instantiated before they are needed. With this variant, we
define the dependency of a service only in one place (the constructor). Imagine now if we change the constructor of a specific service:
We don’t have to care about the instantiation order, it will just work!

Note: (1) We can also generate `impls` (right side) using the build system or figure it out at runtime; (2) the left implementation would
also be totally fine, if we generated that code on each build (though with the risk that someone relies on a specific ordering).