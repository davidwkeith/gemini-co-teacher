# Introduction to Object-Oriented Programming with Python
### A High School CS Course | Adapted from AP Computer Science A

---

## Course Overview

This course teaches object-oriented programming (OOP) using Python, structured around
the same conceptual pillars as AP Computer Science A. Students coming from AP CSP
(JavaScript) will deepen their understanding of software design, algorithms, and
data structures — now through a strongly typed, class-based Python lens.

**Prerequisites**: AP Computer Science Principles (JavaScript) or equivalent  
**Tools**: Chromebook, [Replit](https://replit.com) or [code.org](https://code.org) IDE, Google Classroom  
**Language**: Python 3.10+

---

## Unit 1 — OOP Basics with Python Objects

**Driving Question**: How do we model real-world things in code?

### Topics
- What is an object? Classes vs. instances
- Creating objects with `class` and `__init__`
- Instance variables and `self`
- Calling methods on objects
- Algorithms: sequence, selection (`if/elif/else`), iteration (`for`, `while`)
- Docstrings and inline comments (`"""`, `#`)

### From JavaScript → Python
| JavaScript | Python |
|---|---|
| `function myFunc() {}` | `def my_func():` |
| `let x = 5` | `x = 5` (dynamic typing) |
| `console.log()` | `print()` |
| `// comment` | `# comment` |

### Sample Code
```python
class Painter:
    """Represents a painter in The Neighborhood."""

    def __init__(self, name, color):
        """Initializes a Painter with a name and brush color."""
        self.name = name
        self.color = color

    def paint(self):
        """Paints a stroke using the painter's color."""
        print(f"{self.name} paints a stroke in {self.color}.")


my_painter = Painter("Alex", "blue")
my_painter.paint()
```

### Key Resources
- [Python `class` docs](https://docs.python.org/3/tutorial/classes.html)
- [CS Awesome OOP Unit](https://csawesome.org)

---

## Unit 2 — Class Design

**Driving Question**: How do we build well-designed, reusable classes?

### Topics
- Constructors (`__init__`) with default parameters
- Private vs. public conventions (`_name`, `__name`)
- Getters and setters (accessors/mutators) using `@property`
- `__str__` and `__repr__` (equivalent to Java's `toString()`)
- Class variables vs. instance variables
- The `self` keyword in depth

### Sample Code
```python
class Actor:
    """Represents a Theater actor."""

    theater_name = "The Grand Theater"  # class variable

    def __init__(self, name, role="understudy"):
        self._name = name        # private by convention
        self._role = role

    @property
    def name(self):
        return self._name

    @property
    def role(self):
        return self._role

    @role.setter
    def role(self, new_role):
        if isinstance(new_role, str):
            self._role = new_role

    def __str__(self):
        return f"{self._name} plays {self._role} at {Actor.theater_name}"
```

### Key Concepts
- [`@property` decorator](https://docs.python.org/3/library/functions.html#property)
- [`__str__` vs `__repr__`](https://docs.python.org/3/reference/datamodel.html#object.__repr__)
- [Python naming conventions (PEP 8)](https://peps.python.org/pep-0008/)

---

## Unit 3 — Lists & Algorithms

**Driving Question**: How do we store and process collections of data responsibly?

### Topics
- Python lists: creation, indexing, slicing
- List traversal with `for` loops and `range()`
- Common algorithms: min/max, sum, count, search
- Preconditions and postconditions (docstring contracts)
- Introduction to algorithmic complexity (big-picture)
- Ethical data considerations: privacy, bias in datasets

### Sample Code
```python
def find_max(numbers):
    """
    Returns the maximum value in a non-empty list of numbers.

    Precondition:  len(numbers) >= 1
    Postcondition: returns the largest int/float in numbers
    """
    max_val = numbers[0]
    for num in numbers[1:]:
        if num > max_val:
            max_val = num
    return max_val
```

### Ethics Connection
- Where does student data go? Who owns it?
- Discuss: [ACM Code of Ethics](https://www.acm.org/code-of-ethics)

---

## Unit 4 — Logic & Conditions

**Driving Question**: How do computers make decisions?

### Topics
- Boolean expressions: `True`, `False`, comparisons
- `==` vs `is` (identity vs. equality — Python's version of `==` vs `.equals()`)
- Logical operators: `and`, `or`, `not`
- De Morgan's Laws: `not (A and B)` ≡ `(not A) or (not B)`
- Short-circuit evaluation
- Nested conditionals and guard clauses

### JavaScript → Python Comparison
| Concept | JavaScript | Python |
|---|---|---|
| Logical AND | `&&` | `and` |
| Logical OR | `\|\|` | `or` |
| Logical NOT | `!` | `not` |
| Strict equality | `===` | `==` |
| Reference equality | `==` (sometimes) | `is` |

### De Morgan's Practice
```python
# These are logically equivalent:
not (is_raining and is_cold)
(not is_raining) or (not is_cold)
```

---

## Unit 5 — 2D Lists & Image Data

**Driving Question**: How do we work with grid-based data?

### Topics
- Creating 2D lists (lists of lists)
- Row-major vs. column-major traversal
- Standard algorithms on 2D data: totals, searches, transformations
- Image manipulation as a 2D array of pixels (RGB tuples)
- Using [Pillow](https://pillow.readthedocs.io/en/stable/) for image processing

### Sample Code
```python
# Traversing a 2D list
grid = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for row in grid:
    for value in row:
        print(value, end=" ")
    print()

# Image pixel manipulation with Pillow
from PIL import Image

img = Image.open("photo.jpg")
pixels = img.load()
width, height = img.size

for y in range(height):
    for x in range(width):
        r, g, b = pixels[x, y]
        gray = (r + g + b) // 3
        pixels[x, y] = (gray, gray, gray)  # grayscale

img.save("grayscale.jpg")
```

---

## Unit 6 — Inheritance & Polymorphism

**Driving Question**: How do we reuse and extend class behavior?

### Topics
- Inheritance with `class Child(Parent):`
- Overriding methods
- `super().__init__()` to call parent constructors
- `isinstance()` and type checking
- Polymorphism: calling the same method on different object types
- Abstract base classes with `abc.ABC`
- Composition vs. inheritance trade-offs

### Sample Code
```python
class Performer:
    """Base class for all performers."""

    def __init__(self, name):
        self.name = name

    def perform(self):
        return f"{self.name} performs."


class Musician(Performer):
    """A performer who plays an instrument."""

    def __init__(self, name, instrument):
        super().__init__(name)
        self.instrument = instrument

    def perform(self):
        return f"{self.name} plays the {self.instrument}."


class Dancer(Performer):
    def perform(self):
        return f"{self.name} dances gracefully."


# Polymorphism in action
cast = [Musician("Maya", "violin"), Dancer("Leo")]
for member in cast:
    print(member.perform())
```

---

## Unit 7 — Dictionaries, Sets & Text Processing

**Driving Question**: How do we efficiently store and retrieve structured data?

### Topics
- Python `dict`: key-value pairs, CRUD operations
- Python `set`: uniqueness, membership testing
- String methods: `.split()`, `.strip()`, `.lower()`, `.replace()`
- f-strings and string formatting
- List comprehensions
- Text analysis: word counts, frequency maps
- Introduction to docstring standards ([Google style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings))

### Sample Code
```python
def word_frequency(text):
    """
    Returns a dictionary of word frequencies from a string.

    Args:
        text: A string of space-separated words.

    Returns:
        A dict mapping each word (lowercase) to its count.
    """
    words = text.lower().split()
    freq = {}
    for word in words:
        freq[word] = freq.get(word, 0) + 1
    return freq

# Using a comprehension
cleaned = [w.strip(".,!") for w in "Hello, world! Hello.".split()]
```

---

## Unit 8 — Methods, Recursion & Decomposition

**Driving Question**: How do we break complex problems into elegant solutions?

### Topics
- Function decomposition: single responsibility
- Default parameters and keyword arguments
- `*args` and `**kwargs` (Python's flexible parameter system)
- Recursion: base case, recursive case, call stack
- Comparing recursive vs. iterative solutions
- Tracing recursive calls with diagrams

### Sample Code
```python
def factorial(n):
    """
    Returns n! recursively.

    Base case:    n == 0 → return 1
    Recursive:    n > 0  → return n * factorial(n - 1)
    """
    if n == 0:
        return 1
    return n * factorial(n - 1)


def fibonacci(n, memo={}):
    """Returns the nth Fibonacci number using memoization."""
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]
```

---

## Unit 9 — Search, Sort & Efficiency

**Driving Question**: How do we measure and improve algorithm performance?

### Topics
- Linear search vs. binary search
- Bubble sort, selection sort, insertion sort (conceptual + implementation)
- Python built-ins: `sorted()`, `.sort()`, `key=` parameter
- Big-O notation: O(1), O(n), O(n²) — informal introduction
- Statement counting
- Privacy and security: sorting sensitive data, data minimization

### Sample Code
```python
def binary_search(sorted_list, target):
    """
    Searches a sorted list for target using binary search.

    Args:
        sorted_list: A sorted list of comparable items.
        target:      The item to search for.

    Returns:
        The index of target, or -1 if not found.
    """
    low, high = 0, len(sorted_list) - 1
    while low <= high:
        mid = (low + high) // 2
        if sorted_list[mid] == target:
            return mid
        elif sorted_list[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

---

## Unit 10 — Capstone & AI Tools

**Driving Question**: How do professional developers build and ship real software?

### Topics
- Git & GitHub: version control basics, `commit`, `push`, `pull`
- Working with external APIs (e.g., OpenWeatherMap, NASA)
- Introduction to AI tools: prompt engineering, code review with LLMs
- Computer vision with [OpenCV](https://opencv.org/) or [Teachable Machine](https://teachablemachine.withgoogle.com/)
- Final project: student-designed Python OOP application

### Final Project Requirements
- Minimum 3 interacting classes
- Demonstrates inheritance OR composition
- Includes docstrings on all classes and methods
- Uses at least one external library
- Submitted via GitHub with a `README.md`

---

## Grading Philosophy

| Component | Weight |
|---|---|
| Daily coding exercises | 20% |
| Unit projects | 35% |
| Quizzes & code reviews | 25% |
| Capstone project | 20% |

Peer code review is a **required** part of every unit project submission.

---

## Key Resources

| Resource | Purpose |
|---|---|
| [Python 3 Docs](https://docs.python.org/3/) | Language reference |
| [CS Awesome](https://csawesome.org) | OOP concept reinforcement |
| [Real Python](https://realpython.com) | Tutorials and walkthroughs |
| [PEP 8 Style Guide](https://peps.python.org/pep-0008/) | Code formatting standards |
| [Replit](https://replit.com) | Browser-based IDE (Chromebook-friendly) |
| [Google Style Guide for Python](https://google.github.io/styleguide/pyguide.html) | Docstring and naming conventions |

---

*Adapted from the College Board AP Computer Science A framework. This course is not an AP course and does not include an AP exam.*
