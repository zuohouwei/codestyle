# The Open Closed principle
*All systems change during their lifetimes.*

The **O**pen **C**losed **P**rinciple (**OCP**) states that software should be open for extension but closed to modification. Software modules should be designed in such a way that they don’t need to change. When requirements change, new code is added to extend the behavior while old code remains unchanged. The goal is to reduce or eliminate the seemingly never ending cascade of change that some change in requirements provoke. 

## Example:

<table>
<tr><th width="400px">Better</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

```cpp
class Loan {
public:
  void applyRate(RateCalculator &calc) {
    amount = calc.computePrincipal(amount);
  }
private:
  uint amount;
};

class RateCalculator {
public:
  virtual 
    uint computePrincipal(uint amount) = 0;
   ...
};
```
</pre></td><td><pre lang="cpp">

```cpp
class Loan {
public:
  void applyRate() {
    RateCalculator calc;
    amount = calc.computePrincipal(amount);
   }
private:
  uint amount;
};

class RateCalculator {
public:
  uint computePrincipal(uint amount) {...}
};
```

</pre></td></tr>
</table>

In the bad example if we want to use a new method for computing interest rates we have to modify the applyRate function. In the better example, RateCalculator is an abstract class and the caller decides what type of interest rate calculator to pass-in. Different ways of applying interest rates are now possible by passing-in previously unknown types of interest rate calculators. 

Many of the **OOP** heuristics are guided at least in part by the desire to limit the impact of code changes. Using RTTI, public member variables or global variables means changes are more complex. In the same manner, excessive use of case statements and if/else statements make code more likely to change. That is the reverse of what **OCP** stands for.

It is obvious, that no significant program can be 100% closed to change. Making code closed to change must be therefore strategic. The developer must choose for which kinds of changes the software can be closed against and where making code extensible is most beneficial. Misplaced extension support leads to unneeded complexity. Like everything else in programming, experience and domain knowledge help in making the better decisions.
