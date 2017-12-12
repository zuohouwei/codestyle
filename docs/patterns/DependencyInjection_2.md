[Patterns](../Patterns.md)

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