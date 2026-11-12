# Practice 2 – Integrated Itinerary and Fare Engine

**Course:** Languages and Paradigms of Computation  
**University:** EAFIT

### Team Members
- Samuel Posada López
- Jerónimo Machado Leal

### Compilation

Compile using C++17:

```bash
g++ -std=c++17 -Wall -Wextra -o practice main.cpp
```

Run:

```bash
./practice
```

### Defence Questions

**1. Why must the TransportMode destructor be virtual?**

Because the program uses `std::unique_ptr<TransportMode>` to manage derived objects. A virtual destructor ensures that the correct derived destructor is called when an object is deleted through a base-class pointer, preventing undefined behavior.

**2. Why use STL algorithms and lambda expressions instead of explicit loops?**

STL algorithms make the code more readable, reusable, and maintainable. Functions such as `std::accumulate`, `std::count_if`, and `std::for_each` handle iteration, while lambda expressions define the operations performed without requiring manual loops.
