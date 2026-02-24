---
marp: true
theme: gaia
class: invert
paginate: true
---

<style>
section {
	font-size: 1.9rem;
}

h1 {
	font-size: 3.5rem !important;
	height: 100%;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}

h2 {
	font-size: 2.25rem !important;
}


</style>

<style scoped>
	h1 {
		height: unset;
		display: block;
	}

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
	}
</style>

# Class Customization

Making classes feel natural to use

---

# Part 7 - Class Customization

---

## What is Class Customization?

**Class customization:** Control how instances behave for common operations

- How instances are printed
- How instances are compared
- How operators work with instances

Uses special methods (magic methods) with `__name__` syntax.

---

## The **str**() Method

Control how `print()` displays your object:

```python
class Toy:
    def __init__(self, name, price, min_age):
        self.name = name
        self.price = price
        self.min_age = min_age

truck = Toy("Monster Truck XX", 14.99, 5)
print(truck)
# Output: <__main__.Toy instance at 0xb74cb98c>
```

Not very helpful! Let's customize it.

---

## Implementing **str**()

Define `__str__()` to return a nice description:

```python
class Toy:
    def __init__(self, name, price, min_age):
        self.name = name
        self.price = price
        self.min_age = min_age

    def __str__(self):
        return (f"{self.name} costs only ${self.price:.2f}. "
                f"Not for children under {self.min_age}!")

truck = Toy("Monster Truck XX", 14.99, 5)
print(truck)
# Output: Monster Truck XX costs only $14.99.
#         Not for children under 5!
```

---

## Another **str**() Example

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __str__(self):
        return f"{self.name} (GPA: {self.gpa:.2f})"

alice = Student("Alice Johnson", 3.85)
print(alice)
# Output: Alice Johnson (GPA: 3.85)

# Without __str__():
# Output: <__main__.Student object at 0x...>
```

---

## Operator Overloading

**Operator overloading:** Redefine how operators work with your class

Example: Make `<` work with your custom class

```python
class Time:
    def __init__(self, hours, minutes):
        self.hours = hours
        self.minutes = minutes

    def __str__(self):
        return f"{self.hours}:{self.minutes:02d}"

    def __lt__(self, other):
        """Less than comparison"""
        if self.hours < other.hours:
            return True
        elif self.hours == other.hours:
            if self.minutes < other.minutes:
                return True
        return False

time1 = Time(9, 15)
time2 = Time(10, 40)

if time1 < time2:
    print(f"{time1} is earlier")
# Output: 9:15 is earlier
```

---

## How Operator Overloading Works

When you write `time1 < time2`:

1. Python calls `time1.__lt__(time2)`
2. `self` = `time1` (left side)
3. `other` = `time2` (right side)
4. Returns `True` or `False`

```python
# These are equivalent:
result = time1 < time2
result = time1.__lt__(time2)  # Same thing!
```

---

## Rich Comparison Methods

**Table of comparison operators:**

| Method                | Operator | Meaning               |
| --------------------- | -------- | --------------------- |
| `__lt__(self, other)` | `<`      | Less than             |
| `__le__(self, other)` | `<=`     | Less than or equal    |
| `__gt__(self, other)` | `>`      | Greater than          |
| `__ge__(self, other)` | `>=`     | Greater than or equal |
| `__eq__(self, other)` | `==`     | Equal to              |
| `__ne__(self, other)` | `!=`     | Not equal to          |

---

## Complete Comparison Example

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __str__(self):
        return f"{self.name}: {self.gpa:.2f}"

    def __lt__(self, other):
        return self.gpa < other.gpa

    def __eq__(self, other):
        return self.gpa == other.gpa

alice = Student("Alice", 3.85)
bob = Student("Bob", 3.50)
carol = Student("Carol", 3.85)

print(bob < alice)      # True (3.50 < 3.85)
print(alice <= carol)   # True (3.85 <= 3.85)
print(alice == carol)   # True (3.85 == 3.85)
```

---

## Practical Example: Time Comparison

```python
class Time:
    def __init__(self, hours, minutes):
        self.hours = hours
        self.minutes = minutes

    def __str__(self):
        return f"{self.hours}:{self.minutes:02d}"

    def __lt__(self, other):
        if self.hours != other.hours:
            return self.hours < other.hours
        return self.minutes < other.minutes
```

---

## Finding Earliest Time

```python
times = [Time(10, 40), Time(12, 15), Time(9, 15)]

min_time = times[0]
for t in times:
    if t < min_time:    # Uses __lt__()
        min_time = t

print(f"Earliest: {min_time}")  # Uses __str__()
# Output: Earliest: 9:15
```

---

## Real Example: Product Class

```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def __str__(self):
        return f"{self.name} (${self.price:.2f})"

    def __lt__(self, other):
        return self.price < other.price

    def __eq__(self, other):
        return self.price == other.price
```

---

## Comparing Products

```python
item1 = Product("Widget", 9.99)
item2 = Product("Gadget", 14.99)
item3 = Product("Doohickey", 9.99)

print(item1 < item2)     # True (9.99 < 14.99)
print(item1 == item3)    # True (9.99 == 9.99)
print(item2 > item1)     # True
```

---

## Special Methods Summary

**Most commonly used:**

- `__str__()` - How to print the object
- `__lt__()`, `__eq__()` - How to compare objects
- `__init__()` - Constructor (already covered)

**Other possible customizations:**

- `__add__()` - Operator `+`
- `__sub__()` - Operator `-`
- `__mul__()` - Operator `*`
- `__len__()` - Built-in `len()` function
- `__getitem__()` - Array indexing `[index]`

---

## Best Practices

**Use special methods to:**

- Make your class feel natural to use
- Support Python conventions
- Enable comparisons and operations

```python
# Good - feels natural
print(student)      # Uses __str__()
if time1 < time2:   # Uses __lt__()
    pass

# Bad - awkward
print(student.get_string())
if student.is_less_than(time2):
    pass
```

---

## Summary: Classes & Attributes

**Classes and Instances:**

- Classes are blueprints; instances are objects
- `__init__` constructor initializes new instances
- Parameters passed to `__init__` become attributes

**Attributes:**

- **Instance attributes:** Unique to each object (`self.name`)
- **Class attributes:** Shared by all instances (in class body)
- Access with dot notation: `object.attribute`

---

## Summary: Methods & Constructors

**Methods:**

- Always include `self` as first parameter
- Access instance data via `self`
- Call other methods via `self.method()`

**Constructors:**

- Can have parameters beyond `self`
- Parameters become instance attributes
- Default values support common use cases
- Required parameters must come first

---

## Summary: Interface & Customization

**Class Interface:**

- **Public methods:** Used by programmers (no underscore prefix)
- **Private methods:** Internal only (prefix with `_`)
- **Information hiding:** Show only what's necessary
- **ADT concept:** Data type with well-defined operations

**Class Customization:**

- `__str__()` - Controls how objects are printed
- **Rich comparison methods** - Overload comparison operators
- Makes classes feel natural to use

---

## Summary: Why Use OOP?

**Benefits of Object-Oriented Programming:**

- **Organization:** Related data and functions grouped
- **Reusability:** Create many instances from one class
- **Clarity:** Code shows what objects do
- **Maintainability:** Changes in one place affect all uses
- **Flexibility:** Can improve internals without breaking users' code
- **Natural syntax:** Objects work like built-in types
