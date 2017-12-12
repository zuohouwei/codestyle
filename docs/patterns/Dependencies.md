[Patterns](../Patterns.md)

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
