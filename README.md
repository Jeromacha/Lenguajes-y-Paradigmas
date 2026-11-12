# Integrated Itinerary and Fare Engine
## Metro System of the Valle de Aburrá

**Universidad EAFIT**  
**Course:** Languages and Paradigms of Computation  
**Practice:** Second Practice – 2026-2

### Team Members
- Samuel Posada López
- Jerónimo Machado Leal

## 1. Project Description

This project implements an integrated itinerary and fare calculation system for the Metro System of the Valle de Aburrá using C++17.

The program calculates transportation fares according to passenger profiles, transportation modes, and integration rules.

The implementation demonstrates object-oriented programming concepts such as inheritance, polymorphism, abstract classes, virtual functions, and the Non-Virtual Interface (NVI) pattern.

It also uses the C++ Standard Template Library (STL), lambda expressions, and smart pointers.

## 2. Transportation Modes

The system supports five transportation modes:

- **MetroLine:** Standard metro service.
- **TramLine:** Tram service.
- **CableLine:** Standard cable transportation.
- **TouristCable:** Tourist cable with an additional surcharge and no integration benefits.
- **FeederRoute:** Free feeder transportation that does not open an integration window.

All transportation modes inherit from the abstract class `TransportMode`.

## 3. Passenger Profiles

The system implements five passenger profiles:

| Passenger Profile | Fare Rule |
|---|---|
| Frequent passenger | Standard fare |
| Municipal student | 1,600 COP when permitted |
| Senior citizen | Standard fare minus 490 COP |
| Person with disability | Standard fare minus 1,100 COP |
| Occasional passenger | Standard fare plus 580 COP |

All fares are guaranteed to be non-negative through the `fareOn()` method.

## 4. Integration Rules

The system applies the following rules:

1. The first eligible validation pays the corresponding fare and opens a 90-minute integration window.
2. Up to two transfers within this window are free.
3. Transportation modes that do not allow integration always charge their corresponding fare without modifying the window.
4. Modes that do not open an integration window charge their fare without modifying the current integration state.
5. When the integration window expires or the two free transfers are exhausted, the next eligible validation starts a new window.

The itinerary is sorted chronologically before calculating the charges.

## 5. Compilation and Execution

The project requires a compiler compatible with C++17.

Compile the program using:

```bash
g++ -std=c++17 -Wall -Wextra -o practice main.cpp
```

Execute it on Linux or macOS:

```bash
./practice
```

On Windows:

```bash
.\practice.exe
```

The program can also be executed using OnlineGDB with C++17 selected.

No user input is required.

## 6. STL Algorithms Used

The implementation uses the following algorithms:

- `std::sort`: Sorts itinerary legs chronologically.
- `std::accumulate`: Calculates total payments and joins strings.
- `std::count_if`: Counts free transfers.
- `std::for_each`: Processes collections and generates reports.
- `std::find_if`: Finds the first itinerary leg with a positive charge.

Lambda expressions are used to define the behavior of these algorithms.

The system also uses `std::map` to group payments by transportation service type and `std::function` to inject filtering policies.

## 7. Design Decisions and Oral Defence

### Question 1: Why must the TransportMode destructor be virtual?

The destructor of `TransportMode` must be virtual because transportation objects are managed through pointers to the base class.

The program uses `std::unique_ptr<TransportMode>` to manage objects belonging to different derived classes.

When an object is destroyed through a base-class pointer, a virtual destructor ensures that the destructor of the derived class is executed correctly before the base-class destructor.

Without a virtual destructor, deleting a derived object through a base-class pointer would cause undefined behavior, potentially preventing proper resource cleanup.

Therefore, the virtual destructor is necessary for correct memory management when using inheritance and polymorphism.

### Question 2: What advantages do STL algorithms and lambda expressions provide compared to explicit loops?

STL algorithms allow operations on collections to be expressed clearly without manually implementing the iteration logic.

For example, `std::accumulate` calculates the total amount paid, while `std::count_if` counts the number of free transfers.

Lambda expressions allow us to define specific operations directly where they are needed.

This approach provides several advantages:

- **Readability:** The purpose of each operation is easier to understand.
- **Reusability:** Standard algorithms can be applied to different collections.
- **Maintainability:** The code is easier to modify and extend.
- **Reduced complexity:** Less manual iteration code is required.
- **Separation of responsibilities:** The STL handles iteration while lambda expressions define the operation performed.

In this project, these features help implement the reporting functionality without explicit loops.

## 8. Additional Object-Oriented Design

### Non-Virtual Interface (NVI)

The `Passenger` class implements the Non-Virtual Interface pattern.

The public method `fareOn()` is non-virtual and calls the protected virtual method `computeFare()`.

Each passenger profile can customize its fare calculation by overriding `computeFare()`, while `fareOn()` guarantees that the final fare is never negative.

### Polymorphism

The program uses virtual methods to allow transportation modes and passenger profiles to define their own behavior.

This avoids using `dynamic_cast`, `typeid`, or comparisons between class names.

### Memory Management

The `Network` class stores transportation modes using `std::unique_ptr`.

Objects are created using `std::make_unique`, ensuring automatic memory management without manually calling `new` or `delete`.

## 9. Expected Results

For the provided itinerary, the program produces:

| Result | Value |
|---|---|
| Frequent passenger total | 20,640 COP |
| Municipal student total | 17,800 COP |
| Senior citizen total | 19,170 COP |
| Free transfers | 2 |

These results correspond to the expected output specified in the practice instructions.

---

**Universidad EAFIT – Systems Engineering – 2026-2**
