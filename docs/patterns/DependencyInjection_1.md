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
