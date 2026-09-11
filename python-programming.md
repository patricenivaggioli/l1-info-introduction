# Python Programming — Concepts & Algorithmic Thinking

A refresher for students with 1–2 years of Python, bridging language mechanics and algorithmic reasoning.

## 1. Python's Mental Model

Python is **dynamically typed**, **interpreted**, and **object-oriented** — everything is an object, including functions and classes. Three mental shifts:

- **Names, not variables** — a name is a label pointing to an object. `a = [1, 2]; b = a` makes `b` point to the *same* list, not a copy. Mutating `b` mutates `a`.
- **Mutability matters** — `list`, `dict`, `set` are mutable; `tuple`, `str`, `frozenset` are immutable. This distinction drives correctness, performance, and hashability.
- **Reference semantics** — function arguments are passed by object reference. Mutating a mutable argument inside a function affects the caller; reassigning it does not.

```python
def add_item(lst):
    lst.append(4)        # caller sees the change (mutation)

def replace(lst):
    lst = [10, 20]       # caller sees nothing (rebinding)

data = [1, 2, 3]
add_item(data)           # data is now [1, 2, 3, 4]
replace(data)            # data is still [1, 2, 3, 4]
```

## 2. Core Data Structures & Complexity

Choosing the right structure is an algorithmic decision before it is a coding one.

| Structure | Access | Search | Insert | Delete | When to use |
|-----------|--------|--------|--------|--------|-------------|
| `list` | O(1) by index | O(n) | O(n) front / O(1) end | O(n) | Ordered, index-based access |
| `dict` | O(1) by key | O(1) | O(1) | O(1) | Key-value lookups, fast membership |
| `set` | — | O(1) | O(1) | O(1) | Deduplication, fast membership tests |
| `deque` | O(1) both ends | O(n) | O(1) front & back | O(1) ends | Queues, BFS, sliding windows |
| `heapq` | O(1) peek | O(n) | O(log n) push/pop | O(log n) | Priority queue, top-k problems |

**Insight** — if your code does `if x in my_list` inside a loop, you likely have O(n²). Switch the list to a `set` and it becomes O(n). The algorithm did not change; the data structure did.

## 3. Iteration & Comprehensions

Python favours expressive iteration:

```python
# List comprehension — fast, readable
squares = [x * x for x in range(10) if x % 2 == 0]

# Generator — lazy, memory-efficient
squares_gen = (x * x for x in range(10))

# enumerate when you need the index
for i, value in enumerate(data):
    ...

# zip to iterate in parallel
for name, age in zip(names, ages):
    ...
```

**Algorithmic note** — generators produce values on demand (O(1) memory), making them ideal for streaming large datasets or infinite sequences. A list comprehension would materialise everything in memory at once.

## 4. Functions: Scope, Closures, Decorators

- **Scope (LEGB)** — Local → Enclosing → Global → Built-in. Python resolves names in this order.
- **Closures** — a function defined inside another captures the enclosing variables.

```python
def make_counter():
    count = 0
    def step():
        nonlocal count
        count += 1
        return count
    return step
```

- **Decorators** — a function that wraps another to add behaviour without changing its code.

```python
def timed(fn):
    import time
    def wrapper(*args, **kwargs):
        t0 = time.perf_counter()
        result = fn(*args, **kwargs)
        print(f"{fn.__name__}: {time.perf_counter() - t0:.4f}s")
        return result
    return wrapper

@timed
def slow_func():
    ...
```

**Why it matters** — decorators separate concerns (timing, logging, caching) from logic. This is the same principle behind `@functools.lru_cache`, which memoises results and turns naive recursion into dynamic programming automatically.

## 5. Algorithmic Thinking

Writing code that works is not the same as writing code that scales. Three lenses to evaluate any solution:

### Complexity Analysis

Estimate how time and space grow with input size *n*:

- **O(1)** — hash table lookup
- **O(log n)** — binary search, balanced tree operations
- **O(n)** — single pass over data
- **O(n log n)** — efficient sorting (Timsort, merge sort)
- **O(n²)** — nested loops, naive pairwise comparison
- **O(2ⁿ)** — naive recursion without memoisation

### Patterns to Recognise

| Pattern | Signal | Typical approach |
|---------|--------|------------------|
| Two pointers | Sorted array / palindromes | Shrink from both ends |
| Sliding window | Contiguous subarray / substring | Expand and contract a window |
| Hash map | Counting, lookup, pairing | Trade space for O(1) lookups |
| Divide & conquer | Problem splits into independent subproblems | Recursion (merge sort, quicksort) |
| Dynamic programming | Overlapping subproblems + optimal substructure | Memoise or build a table bottom-up |
| Greedy | Local optimal → global optimal | Sort and iterate, prove correctness |

### Example: Fibonacci — Three Algorithms, Three Complexities

```python
# Naive recursion — O(2ⁿ) time, O(n) stack
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)

# Memoisation (top-down DP) — O(n) time, O(n) space
from functools import lru_cache
@lru_cache
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)

# Iterative (bottom-up DP) — O(n) time, O(1) space
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

**The lesson** — the same problem admits radically different complexities. The algorithm you choose matters more than the speed of the language.

## 6. OOP in Python

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):          # overridden by subclasses
        raise NotImplementedError

class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow"
```

Key points:

- **`__init__`** — constructor; sets instance state.
- **Inheritance** — `Dog` reuses `Animal`'s interface and overrides behaviour.
- **Polymorphism** — any `Animal` can `speak()`; the right method resolves at runtime.
- **Dunder methods** (`__repr__`, `__eq__`, `__len__`...) let your classes integrate with built-in operators and functions.
- Prefer **composition over inheritance** when behaviour does not fit a true "is-a" relationship — a `Car` *has an* `Engine`, rather than `Car` *is an* `Engine`.

## 7. Error Handling & Robustness

```python
try:
    result = 10 / x
except ZeroDivisionError:
    result = float("inf")
except TypeError as e:
    print(f"Bad input: {e}")
else:
    print("No error")
finally:
    cleanup()
```

- Catch **specific** exceptions, not bare `except:` — the latter hides bugs.
- Use `else` for code that runs only on success, and `finally` for cleanup that always runs.
- Raise your own exceptions with `raise ValueError("message")` — fail loudly and early.

## 8. Testing

```python
# test_math.py
import pytest

def test_add():
    assert add(2, 3) == 5

def test_divide_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

- **Unit tests** check individual functions in isolation.
- Use `pytest` — simple `assert` statements, parametrised tests, and fixtures.
- Test edge cases: empty input, negatives, large values, boundary conditions.

**Algorithmic angle** — test not just correctness but performance. A correct answer does not guarantee the solution scales. Add timing or size-based assertions to catch O(n²) regressions.

## 9. Idiomatic Python — Cheat Sheet

| Idiom | Instead of |
|-------|------------|
| `for item in lst:` | `for i in range(len(lst)): lst[i]` |
| `if key in d:` | `if key in d.keys():` |
| `a, b = b, a` | temp variable swap |
| `collections.Counter` | manual counting loop |
| `any()` / `all()` | loop + flag variable |
| `str.join(list)` | `+` concatenation in a loop |
| `with open(f) as fh:` | `open()` without `close()` |

## 10. Key Takeaways

1. **Data structure choice is an algorithmic choice** — know your complexities.
2. **Mutability and references** explain most subtle Python bugs.
3. **Generators and comprehensions** make code both readable and memory-efficient.
4. **Complexity analysis** tells you whether your solution scales, not just whether it works.
5. **Pattern recognition** (two pointers, DP, greedy, divide & conquer) is the bridge between a problem statement and an efficient solution.
6. **Test correctness and performance** — a correct-but-slow solution is still wrong at scale.
