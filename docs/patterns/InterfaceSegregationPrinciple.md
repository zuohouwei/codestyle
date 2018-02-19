[Patterns](../Patterns.md)

# The Interface Segregation Principle
Clients should not depend on interfaces they do not use.

The **I**nterface **S**egregation **P**rinciple (**ISP**) states that no client should be forced to depend upon methods it doesn’t use.
Large interfaces, with multiple methods force clients to depend on methods and types which are not relevant to them.
Small changes in some parts of the program would lead to unrelated parts of the program to need further change or recompilation.
Excessive recompilation is a symptom of **ISP** violations.

## Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
class Conection {
public:
  virtual void Open(IPAddress& addr) = 0;
  virtual void Close() = 0;
};
class DataReceiver {
public:
  virtual 
    bool Receive(ByteArray& buffer) = 0;
};
class Socket: public Connection, 
              public DataReceiver {...}
...
void ReceiveData(DataReceiver& sock) { 
  ByteArray& buffer;
  sock.receive(buffer);
}
```
</pre></td><td><pre lang="cpp">

```cpp
class Socket {
public:
  void Open(IPAddress& addr);
  bool Close();
  bool Receive(ByteArray& buffer);
  ...
};
...
void ReceiveData(Socket& sock) {
  ByteArray& buffer;
  sock.receive(buffer);
...
}
```

</pre></td></tr>
</table>

In the bad example, clients depend on *IPAddress* and *ByteArray*. In the good example, clients can access the socket object through
the *Connection* or *DataReceiver* interface thus reducing their dependencies. In the good example, changes in the *IPAddress* class
would no longer trigger recompilation in the ReceiveData method and its clients.

The **ISP** promotes separation between different clients of an interface. When a client depends upon a class that contains interfaces
that the client does not use but other clients use, it is subject to all the changes that the other clients force upon the class.
Sometimes this means "just another recompilation", some other times it means participating in a seemingly never-ending avalanche of change.

In order to separate interfaces, clients of an object should stop accessing the object directly by calling functions in its interface.
They should either access it through delegation, or through a base class of the object. Interfaces are segregated by introducing a new level of abstraction.
