# Anti-Patterns

**Anti–Patterns** - Commonly used programming practices that have proven to be ineffective, inefficient, or otherwise counter–productive

### Software Design Anti-Patterns

* **Input kludge** - Lack of input validation
* **Interface bloat** - Making an interface so complicated that it is hard to use
* **Race hazard** - Two, or more, events dependent on each other. Event A waiting for Event B, while Event B is waiting for Event A

### Object-Oriented Design Anti-Patterns

* **Circular dependency** - Introducing unnecessary direct, or indirect, mutual dependencies between objects or software modules. Class A calls Class B, then Class B calls Class A
* **God object** - An object that has too much information, or too much responsibility. Too many unrelated methods in a single class. "Single-purpose principle"

### Programming Design Anti-Patterns

* **Hard coding** - Embedding assumptions about the environment of a system in its implementation. "Dependency inversion" principle
* **Magic numbers** - Including unexplained numbers in algorithms / code
* **Magic strings** - Including literal strings in code, eg: for comparisons

### Methodological Design Anti-Patterns

* **Copy and paste programming** - Copying and modifying existing code without creating more generic solutions
* **Reinventing the wheel** - Failing to adopt an existing, adequate solution and, instead adopting a custom solution which provides no additional benefit, and wastes time and effort
