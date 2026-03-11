# Unit 6 FRQ — The Animal Shelter
### Introduction to OOP with Python | Inheritance & Polymorphism

**Time allowed**: 20–25 minutes  
**Topics assessed**: Inheritance, `super()`, method overriding, `__str__`, polymorphism

---

## Background

Happy Paws Animal Shelter tracks animals awaiting adoption. You are given the
following fully-working `Animal` base class. **Do not modify it.**

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    """Abstract base class representing a shelter animal."""

    def __init__(self, name, age):
        self._name = name
        self._age  = age

    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age

    @abstractmethod
    def is_senior(self):
        """Returns True if this animal is considered senior-aged."""
        pass

    def __str__(self):
        return f"{self._name} (age {self._age})"
```

---

## Part A — Code (20 points)

Write **both** of the following classes in the code block below.

### `Dog`
- Inherits from `Animal`
- Constructor takes `name`, `age`, and `breed` (string)
- `is_senior()` returns `True` if the dog is **8 years or older**
- `__str__()` returns: `"Buddy (age 10) — Labrador [Senior]"` if senior,
  or `"Rex (age 3) — Beagle"` if not

### `Cat`
- Inherits from `Animal`
- Constructor takes `name`, `age`, and `indoor` (boolean)
- `is_senior()` returns `True` if the cat is **10 years or older**
- `__str__()` returns: `"Whiskers (age 12) — Indoor [Senior]"` if senior,
  or `"Luna (age 4) — Outdoor"` if not

**Requirements that apply to both classes:**
- Must call `super().__init__()` correctly
- `__str__()` must call `super().__str__()` to get the `name (age N)` portion
- The `[Senior]` tag must only appear when `is_senior()` returns `True`

```python
# YOUR CODE HERE
```

---

## Part B — Short Answer (5 points)

The `adoption_candidates` function below works correctly on a **mixed list**
of `Dog` and `Cat` objects without checking the type of each animal.

```python
def adoption_candidates(animals):
    return [a for a in animals if a.is_senior()]
```

**In 2–4 sentences**: Name the OOP principle that makes this possible and
explain *why* this function works even though `Dog` and `Cat` compute
`is_senior()` using different age thresholds.

```
YOUR ANSWER:
```

---

## Sample Solution (Teacher Copy)

### Part A

```python
class Dog(Animal):
    """Represents a dog available for adoption."""

    def __init__(self, name, age, breed):
        super().__init__(name, age)
        self._breed = breed

    def is_senior(self):
        return self._age >= 8

    def __str__(self):
        base = super().__str__()
        tag  = " [Senior]" if self.is_senior() else ""
        return f"{base} — {self._breed}{tag}"


class Cat(Animal):
    """Represents a cat available for adoption."""

    def __init__(self, name, age, indoor):
        super().__init__(name, age)
        self._indoor = indoor

    def is_senior(self):
        return self._age >= 10

    def __str__(self):
        base     = super().__str__()
        location = "Indoor" if self._indoor else "Outdoor"
        tag      = " [Senior]" if self.is_senior() else ""
        return f"{base} — {location}{tag}"
```

### Part B — Model Answer

This is **polymorphism**. Both `Dog` and `Cat` are subclasses of `Animal` and
each provides its own implementation of `is_senior()`. When
`adoption_candidates` calls `a.is_senior()`, Python dispatches to the correct
version at runtime based on the actual type of the object — not the variable
type. This means the function works correctly on any current or future
`Animal` subclass without modification.

---

## Rubric

### Part A (20 points)

| Criterion | Points |
|---|---|
| `Dog.__init__` calls `super().__init__(name, age)` | 2 |
| `Dog` stores `breed` as instance variable | 1 |
| `Dog.is_senior()` uses correct threshold (`>= 8`) | 2 |
| `Dog.__str__()` calls `super().__str__()` | 2 |
| `Dog.__str__()` includes breed and correct format | 1 |
| `Dog.__str__()` appends `[Senior]` conditionally | 2 |
| `Cat.__init__` calls `super().__init__(name, age)` | 2 |
| `Cat` stores `indoor` as instance variable | 1 |
| `Cat.is_senior()` uses correct threshold (`>= 10`) | 2 |
| `Cat.__str__()` calls `super().__str__()` | 2 |
| `Cat.__str__()` shows Indoor/Outdoor correctly | 1 |
| `Cat.__str__()` appends `[Senior]` conditionally | 2 |

### Part B (5 points)

| Criterion | Points |
|---|---|
| Correctly names **polymorphism** | 2 |
| Explains runtime dispatch (Python picks the right method) | 2 |
| Connects to the fact that subclasses have *different* thresholds | 1 |

### Common Errors
- Using `>` instead of `>=` (off-by-one on threshold)
- `__str__` rebuilds `name (age N)` manually instead of calling `super().__str__()`
- `[Senior]` always appears or never appears (missing conditional)
- Part B names "inheritance" or "encapsulation" instead of "polymorphism"
- Part B explains *what* each method does but not *why the function doesn't need to know the type*