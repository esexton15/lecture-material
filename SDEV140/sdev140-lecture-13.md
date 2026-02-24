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

# Object-Oriented Programming

Organizing code with classes and objects

---

# Part 1 - What is Object-Oriented Programming?

---

## Objects in the Physical World

Objects are groupings of materials:

- Chair = wood + fabric + nails
- TV = plastic + glass + circuits
- Car = metal + rubber + engine

We think in terms of complete objects, not individual materials.

---

## Objects in Programming

We also have groupings:

- **Variables** = data (like materials)
- **Functions** = operations (like actions)

**Objects** = grouping data and functions together

---

## Why Objects?

Without objects, programs become messy:

```python
user1_name = "Alice"
user1_email = "alice@example.com"
user1_age = 20

user2_name = "Bob"
user2_email = "bob@example.com"
user2_age = 25
```

With objects, code is organized:

```python
# With objects - cleaner!
alice = User("Alice", "alice@example.com", 20)
bob = User("Bob", "bob@example.com", 25)
```

---

## Abstraction & Information Hiding

**Abstraction:** Interact with objects at a high level

**Example - An Oven:**

```
User sees: food compartment + heat knob

User doesn't see: heating elements,
                  thermostat circuits,
                  timer mechanisms
```

**Objects hide complexity:**

- Show only what users need
- Hide internal details
- Users interact with public interface

---

## Abstract Data Types (ADT)

**ADT:** A data type with specific, well-defined operations

**Example - Stack:**

```
Operations: push(), pop(), peek()
Everything else is hidden
```

**Python strings are ADTs:**

```python
mystr = "Hello"
mystr.upper()      # PUBLIC operation
mystr.lower()      # PUBLIC operation
# You don't access internal character array directly
```

---

## Built-in Objects in Python

**Everything in Python is an object!**

```python
# String object with data and methods
mystr = "Hello"
mystr.isdigit()    # method
mystr.lower()      # method
len(mystr)         # property

# Integer object
x = 42
x.__add__(8)       # method (used by +)

# List object
items = [1, 2, 3]
items.append(4)    # method
```

We've been using objects all along!

---

# Part 2 - Creating Classes

---

## What is a Class?

**Class:** A blueprint for creating objects

Think of a class like a template or mold.

```
Class = blueprint (like a cookie cutter)
Instance = actual object (like individual cookies)
```

**One class → many instances**

---

## Defining a Class

```python
class ClassName:
    # methods and data go here
    pass
```

**Example - Time class:**

```python
class Time:
    """ A class that represents a time of day """
    def __init__(self):
        self.hours = 0
        self.minutes = 0
```

---

## The **init** Method

**`__init__` = constructor**

Automatically called when you create a new instance.

Responsible for setting up initial state.

```python
class Time:
    """ A class that represents a time of day """
    def __init__(self):
        self.hours = 0      # Create attribute hours
        self.minutes = 0    # Create attribute minutes
```

**`self` = the object being created**

---

## Creating Instances

**Instantiation:** Creating an object from a class

```python
class Time:
    def __init__(self):
        self.hours = 0
        self.minutes = 0

# Create instance
my_time = Time()

# Access attributes with dot notation
my_time.hours = 7
my_time.minutes = 15

print(f"{my_time.hours}:{my_time.minutes:02d}")
# Output: 7:15
```

---

## Dot Notation

`object.attribute` - Access data or methods

```python
my_time.hours        # READ attribute
my_time.hours = 7    # MODIFY attribute

my_time.hours + 5    # USE attribute

mystr.upper()        # CALL method
```

---

## Multiple Instances

Each instance is independent:

```python
class Time:
    def __init__(self):
        self.hours = 0
        self.minutes = 0

time1 = Time()
time1.hours = 7
time1.minutes = 30

time2 = Time()
time2.hours = 12
time2.minutes = 45

print(f"Time 1: {time1.hours}:{time1.minutes:02d}")
print(f"Time 2: {time2.hours}:{time2.minutes:02d}")
```

---

## Class Naming Convention

Use **PascalCase** (capitalize first letter of each word)

```python
# Good class names
class Time:
    pass

class StudentRecord:
    pass

class PDFDocument:
    pass
```

```python
# Bad class names
class time:           # lowercase
class student_record: # snake_case
class PDF:            # all caps
```

---

## Real-World Example: Student Class

```python
class Student:
    """ Represents a student """
    def __init__(self):
        self.name = ""
        self.student_id = 0
        self.gpa = 0.0
        self.courses = []

alice = Student()
alice.name = "Alice Johnson"
alice.student_id = 12345
alice.gpa = 3.8
alice.courses = ["Math", "Science", "History"]

print(f"{alice.name} - GPA: {alice.gpa}")
```

---

## Real-World Example: Book Class

```python
class Book:
    """ Represents a book """
    def __init__(self):
        self.title = ""
        self.author = ""
        self.pages = 0
        self.isbn = ""

book1 = Book()
book1.title = "Python Basics"
book1.author = "John Smith"
book1.pages = 450
book1.isbn = "978-1234567890"

book2 = Book()
book2.title = "Web Development"
book2.author = "Jane Doe"
book2.pages = 520
book2.isbn = "978-0987654321"
```

---

## Benefits of Using Classes

**Organization:** Related data grouped together

**Reusability:** Define once, create many instances

**Maintainability:** Changes in one place affect all instances

**Clarity:** Code shows intent and structure

**Real-world modeling:** Classes mirror how we think

---

## Key Concepts Review

**Class:** Blueprint/template for objects

**Instance:** Individual object created from class

\***\*init**:\*\* Constructor, initializes new instance

**self:** Reference to the instance being created

**Attribute:** Data stored in an object (self.name)

**Dot notation:** Access attributes with `.`

**PascalCase:** Proper naming convention for classes

---

# Part 3 - Instance Methods

---

## What are Instance Methods?

**Instance method:** A function defined inside a class

Methods operate on instance data using `self`

```python
class Time:
    def __init__(self):
        self.hours = 0
        self.minutes = 0

    def print_time(self):  # Instance method
        print(f"{self.hours}:{self.minutes:02d}")

time1 = Time()
time1.hours = 7
time1.minutes = 15
time1.print_time()  # Call the method
# Output: 7:15
```

---

## The self Parameter

**`self` = reference to the instance**

Used to access that instance's attributes and methods

```python
class Time:
    def __init__(self):
        self.hours = 0      # self refers to the instance
        self.minutes = 0    # self refers to the instance

    def print_time(self):           # self is first parameter
        print(self.hours)           # access instance data
        print(self.minutes)         # access instance data

time1 = Time()
time1.print_time()  # Python passes time1 as self
```

---

## Calling Methods with Dot Notation

Method call automatically passes instance as `self`

```python
class Employee:
    def __init__(self):
        self.wage = 0
        self.hours_worked = 0

    def calculate_pay(self):
        return self.wage * self.hours_worked

alice = Employee()
alice.wage = 9.25
alice.hours_worked = 35

pay = alice.calculate_pay()  # alice becomes self
print(f"Pay: ${pay:.2f}")
# Output: Pay: $323.75
```

---

## Using self in Methods

Access other attributes and methods:

```python
class Student:
    def __init__(self):
        self.name = ""
        self.grades = []

    def add_grade(self, grade):
        self.grades.append(grade)

    def get_average(self):
        return sum(self.grades) / len(self.grades)

    def display_student(self):
        avg = self.get_average()  # Call method!
        print(f"{self.name}: {avg:.1f}")
```

---

## Example: Student Methods

```python
alice = Student()
alice.name = "Alice"
alice.add_grade(95)
alice.add_grade(87)
alice.display_student()
# Output: Alice: 91.0

# access instance data via self
# call other methods via self.method()
```

---

## Special Methods (Magic Methods)

Methods with double underscores have special meaning

`__init__` is one example (constructor)

```python
class Time:
    def __init__(self):        # Initialize new instances
        self.hours = 0
        self.minutes = 0

    def __str__(self):         # String representation
        return f"{self.hours}:{self.minutes:02d}"

    def __add__(self, other):  # Addition operation
        # Code to add two Time objects
        pass
```

**Avoid using `__` in your own identifiers** to prevent collisions

---

## Common Error: Forgetting self

**ERROR:** Omitting `self` parameter

```python
class Employee:
    def __init__(self):
        self.wage = 0
        self.hours_worked = 0

    def calculate_pay():  # WRONG! Missing self
        return self.wage * self.hours_worked

alice = Employee()
alice.wage = 9.25
alice.hours_worked = 35
alice.calculate_pay()

# TypeError: calculate_pay() takes 0 positional
# arguments but 1 was given
```

---

## Common Error Explained

Python automatically passes instance as first argument:

```python
# What you write
alice.calculate_pay()

# What Python does internally
Employee.calculate_pay(alice)  # Passes alice!

# If method has no self parameter, it can't accept alice
# Result: "too many positional arguments" error
```

**FIX: Always include `self` as first parameter**

```python
def calculate_pay(self):  # Correct!
    return self.wage * self.hours_worked
```

---

## Real Example: Car Class

```python
class Car:
    def __init__(self):
        self.make = ""
        self.model = ""
        self.speed = 0

    def accelerate(self, amount):
        self.speed += amount
        print(f"Speed: {self.speed} mph")

    def brake(self):
        self.speed = 0
        print("Stopped!")

car = Car()
car.make = "Toyota"
car.model = "Camry"
car.accelerate(20)
car.accelerate(30)
car.brake()
```

---

## Real Example: BankAccount Class

```python
class BankAccount:
    def __init__(self):
        self.owner = ""
        self.balance = 0.0

    def deposit(self, amount):
        self.balance += amount
        print(f"Deposited: ${amount:.2f}")

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            print(f"Withdrew: ${amount:.2f}")
        else:
            print("Insufficient funds")

    def show_balance(self):
        print(f"{self.owner}: ${self.balance:.2f}")

account = BankAccount()
account.owner = "Alice"
account.deposit(500)
account.withdraw(100)
account.show_balance()
```

---

## Benefits of Methods

**Encapsulation:** Data + operations together

**Reusability:** Call method multiple times

**Clarity:** Shows what operations an object supports

**Maintenance:** Logic in one place

```python
# Without methods (data scattered)
bank_balance = 1000
bank_balance = bank_balance + 500  # Where is deposit logic?
bank_balance = bank_balance - 100  # Where is withdraw logic?

# With methods (clear operations)
account.deposit(500)
account.withdraw(100)
```

---

# Part 4 - Class vs Instance Attributes

---

## Two Types of Objects

**Class object:** The blueprint (factory)

**Instance object:** Individual objects created from the blueprint

```python
class Dog:  # This is a class object
    pass

buddy = Dog()   # This is an instance object
fido = Dog()    # This is another instance object
```

---

## Class Attributes

**Class attribute:** Shared by ALL instances

Defined in class scope (not in `__init__`)

```python
class MarathonRunner:
    race_distance = 42.195  # All instances share this

    def __init__(self):
        self.speed = 0

runner1 = MarathonRunner()
runner2 = MarathonRunner()

print(MarathonRunner.race_distance)
print(runner1.race_distance)
print(runner2.race_distance)
# Output: 42.195, 42.195, 42.195
```

---

## Instance Attributes

**Instance attribute:** Unique to each instance

Defined with `self.attribute` in methods

```python
class MarathonRunner:
    race_distance = 42.195  # Shared by all

    def __init__(self):
        self.speed = 0  # Unique to each instance

runner1 = MarathonRunner()
runner1.speed = 7.5

runner2 = MarathonRunner()
runner2.speed = 8.0

print(f"Runner 1: {runner1.speed}")  # 7.5
print(f"Runner 2: {runner2.speed}")  # 8.0
```

---

## Namespace Lookup

**Attribute lookup order:**

1. Check instance namespace
2. If not found, check class namespace

```python
class Student:
    school = "Central High"  # Class attribute

    def __init__(self, name):
        self.name = name    # Instance attribute

alice = Student("Alice")

print(alice.name)      # Found in instance namespace
print(alice.school)    # Not in instance, found in class
# Output: Alice, Central High
```

---

## When Class Attributes Change

Changes affect ALL instances!

```python
class Time:
    gmt_offset = 0  # Class attribute

    def __init__(self):
        self.hours = 0
        self.minutes = 0

    def print_time(self):
        offset_hours = self.hours + self.gmt_offset
        print(f"{offset_hours}:{self.minutes:02d}")

time1 = Time()
time1.hours = 10
time1.minutes = 15

time2 = Time()
time2.hours = 12
time2.minutes = 45
```

---

## When Class Attributes Change (continued)

Printing both instances:

```python
print("GMT:")
time1.print_time()  # 10:15
time2.print_time()  # 12:45

# Change class attribute
Time.gmt_offset = -8  # Pacific Time

print("PST (GMT-8):")
time1.print_time()  # 2:15
time2.print_time()  # 4:45
```

Both instances now use the new offset!

---

## Common Uses of Class Attributes

**Constants used by all instances:**

```python
class Circle:
    PI = 3.14159  # Same for all circles

    def __init__(self, radius):
        self.radius = radius  # Each circle has its own

    def area(self):
        return Circle.PI * self.radius ** 2

c1 = Circle(5)
c2 = Circle(10)

print(c1.area())  # Uses Circle.PI
print(c2.area())  # Uses Circle.PI
```

---

## Accessing via self

You can use `self` to access both types:

```python
class Time:
    gmt_offset = 0  # Class attribute

    def __init__(self):
        self.hours = 0  # Instance attribute

    def print_time(self):
        # Access instance attribute
        print(self.hours)

        # Access class attribute
        print(self.gmt_offset)

time1 = Time()
time1.print_time()  # self finds both!
```

---

## Best Practice: Name Collisions

**Avoid using same name for class and instance attribute**

```python
# CONFUSING - Avoid this!
class Time:
    offset = 0          # Class attribute

    def __init__(self):
        self.offset = 5  # Instance attribute (shadows class!)

# BETTER - Use different names
class Time:
    default_offset = 0      # Class attribute (clear name)

    def __init__(self):
        self.current_offset = 5  # Instance attribute (clear name)
```

When names collide, **instance always wins**

---

## Summary: Class vs Instance

| Aspect         | Class Attribute                 | Instance Attribute       |
| -------------- | ------------------------------- | ------------------------ |
| Scope          | In class body                   | In `__init__` or methods |
| Shared         | All instances                   | Unique to each           |
| Access         | `ClassName.attr` or `self.attr` | `self.attr`              |
| Change affects | All instances                   | Only that instance       |
| Example        | Constants                       | Individual data          |

---

## Summary: Classes in Python

**Classes:**

- Blueprints for creating objects
- `__init__` initializes new instances
- `self` refers to the current instance

---

## Summary: Attributes

**Instance attributes:** Unique to each object (defined with `self`)

**Class attributes:** Shared by all instances (defined in class body)

**Lookup order:** Check instance first, then class

---

## Summary: Methods

**Methods** are functions inside classes

- Always include `self` as first parameter
- Called using dot notation on instances
- Operate on instance data

---

## Summary: Key Concepts

- Objects group data and operations together
- Abstraction hides internal complexity
- Each instance is independent
- Class attributes enable sharing constants
- Always use descriptive names to avoid confusion

---

# Part 5 - Class Constructors with Parameters

---

## Adding Parameters to **init**

`__init__` can accept parameters beyond `self`:

```python
class RaceTime:
    def __init__(self, start_hrs, start_mins,
                       end_hrs, end_mins, distance):
        self.start_hrs = start_hrs
        self.start_mins = start_mins
        self.end_hrs = end_hrs
        self.end_mins = end_mins
        self.distance = distance
```

Each parameter becomes an instance attribute!

---

## Creating Instances with Arguments

Pass arguments when instantiating:

```python
class RaceTime:
    def __init__(self, start_hrs, start_mins,
                       end_hrs, end_mins, distance):
        self.start_hrs = start_hrs
        self.start_mins = start_mins
        self.end_hrs = end_hrs
        self.end_mins = end_mins
        self.distance = distance

# Create instances with specific values
race1 = RaceTime(5, 30, 7, 0, 5.0)
race2 = RaceTime(6, 15, 8, 45, 10.0)

print(f"Race 1: {race1.distance} miles")
print(f"Race 2: {race2.distance} miles")
```

---

## Real Example: RaceTime Class

```python
class RaceTime:
    def __init__(self, start_hrs, start_mins,
                       end_hrs, end_mins, distance):
        self.start_hrs = start_hrs
        self.start_mins = start_mins
        self.end_hrs = end_hrs
        self.end_mins = end_mins
        self.distance = distance

    def get_elapsed_time(self):
        if self.end_mins >= self.start_mins:
            minutes = self.end_mins - self.start_mins
            hours = self.end_hrs - self.start_hrs
        else:
            minutes = 60 - self.start_mins + self.end_mins
            hours = self.end_hrs - self.start_hrs - 1
        return hours, minutes
```

---

## Real Example: RaceTime Methods

```python
    def print_time(self):
        hours, minutes = self.get_elapsed_time()
        print(f"Time to complete: {hours}:{minutes:02d}")

    def print_pace(self):
        hours, minutes = self.get_elapsed_time()
        total_minutes = hours * 60 + minutes
        pace = total_minutes / self.distance
        print(f"Avg pace: {pace:.2f} mins/mile")

race = RaceTime(5, 30, 7, 0, 5.0)
race.print_time()   # Time to complete: 1:30
race.print_pace()   # Avg pace: 18.00 mins/mile
```

---

## Default Parameter Values

Use default values for common states:

```python
class Employee:
    def __init__(self, name, wage=8.25, hours=20):
        """
        Typical new employee is part-time and
        earns minimum wage
        """
        self.name = name
        self.wage = wage
        self.hours = hours

todd = Employee("Todd")
# Uses defaults: wage=8.25, hours=20

jason = Employee("Jason")
# Uses defaults

tricia = Employee("Tricia", 12.50, 40)
# Manager: custom wage and hours
```

---

## Using Default Parameters

```python
class Employee:
    def __init__(self, name, wage=8.25, hours=20):
        self.name = name
        self.wage = wage
        self.hours = hours

    def weekly_pay(self):
        return self.wage * self.hours

employees = [
    Employee("Todd"),           # Part-time, min wage
    Employee("Jason"),          # Part-time, min wage
    Employee("Tricia", 12.50, 40)  # Full-time, higher wage
]

for e in employees:
    pay = e.weekly_pay()
    print(f"{e.name}: ${pay:.2f}/week")
```

---

## Output with Defaults

```
Todd: $165.00/week
Jason: $165.00/week
Tricia: $500.00/week
```

---

## Mixing Required and Default Parameters

**Rules:**

- Required parameters come first
- Default parameters come after
- Can use positional or keyword arguments

```python
class Student:
    def __init__(self, name, gpa=3.5):
        self.name = name
        self.gpa = gpa

alice = Student("Alice")       # Use default
bob = Student("Bob", 3.8)      # Override default
carlos = Student("Carlos", gpa=3.2)  # Keyword
```

---

## Parameter Order: Correct vs Wrong

**CORRECT - Required first:**

```python
def __init__(self, name, gpa=3.5):
    pass
```

**WRONG - Syntax Error!:**

```python
def __init__(self, gpa=3.5, name):
    pass  # Default before required!
```

---

## Real Example: BankAccount Class

```python
class BankAccount:
    def __init__(self, owner, initial_balance=0):
        self.owner = owner
        self.balance = initial_balance
        self.interest_rate = 0.02

alice = BankAccount("Alice")
# Starts with $0 balance

bob = BankAccount("Bob", 1000)
# Starts with $1000

tricia = BankAccount("Tricia", 500)
# Starts with $500
```

---

## Real Example: BankAccount Methods

```python
    def deposit(self, amount):
        self.balance += amount
        print(f"Deposited: ${amount:.2f}")
        return self.balance

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            return True
        return False

alice.deposit(500)      # Alice: $500
bob.withdraw(200)       # Bob: $800
print(f"Bob: ${bob.balance:.2f}")
```

---

## Why Default Parameters Matter

**Flexibility:**

- Support common use cases simply
- Allow specialization when needed

**Real world examples:**

- New employees: standard wage/hours
- New accounts: standard interest rate
- New items: standard quantity

---

## Example: Default Parameters in Use

```python
class Product:
    def __init__(self, name, price, quantity=1):
        self.name = name
        self.price = price
        self.quantity = quantity

item1 = Product("Widget", 9.99)  # qty=1 (default)
item2 = Product("Tool", 24.99, 5)  # qty=5 (specified)
```

---

## Best Practices: Parameter Ordering

1. Required parameters first
2. Default parameters after
3. Most common defaults first

```python
# Good - makes sense
class User:
    def __init__(self, username, email,
                 active=True, role="user"):
        self.username = username
        self.email = email
        self.active = active
        self.role = role
```

---

## Best Practices: Correct Syntax

Parameters with defaults must come AFTER required parameters

```python
# CORRECT
def __init__(self, name, age=18):
    pass

# WRONG - Syntax Error!
def __init__(self, age=18, name):
    pass  # Can't have required after default
```

---

# Part 6 - Class Interfaces

---

## What is a Class Interface?

**Class interface:** The set of methods that programmers use to interact with objects

Think of it as the "public" face of a class.

```python
class Student:
    def __init__(self, name):          # INTERFACE
        self.name = name

    def add_grade(self, grade):        # INTERFACE
        self.grades.append(grade)

    def get_average(self):             # INTERFACE
        return sum(self.grades) / len(self.grades)

# Programmers use these three methods
alice = Student("Alice")
alice.add_grade(95)
avg = alice.get_average()
```

---

## Public vs Private Methods

**Public methods:** Part of the interface, meant for users

**Private methods:** Internal only, helper functions

Prefix private methods with underscore: `_helper()`

```python
class RaceTime:
    def __init__(self, start_hrs, start_mins,
                 end_hrs, end_mins, distance):
        self.start_hrs = start_hrs
        self.start_mins = start_mins
        self.end_hrs = end_hrs
        self.end_mins = end_mins
        self.distance = distance

    # PUBLIC interface
    def print_time(self):
        total_time = self._diff_time()
        hours, minutes = total_time
        print(f"Time: {hours}:{minutes:02d}")

    def print_pace(self):
        total_time = self._diff_time()
        total_mins = total_time[0] * 60 + total_time[1]
        pace = total_mins / self.distance
        print(f"Pace: {pace:.2f} min/mile}")
```

---

## Private Helper Method

```python
    # PRIVATE helper - internal use only
    def _diff_time(self):
        if self.end_mins >= self.start_mins:
            mins = self.end_mins - self.start_mins
            hrs = self.end_hrs - self.start_hrs
        else:
            mins = 60 - self.start_mins + self.end_mins
            hrs = self.end_hrs - self.start_hrs - 1
        return (hrs, mins)

race = RaceTime(9, 30, 10, 3, 5.0)
race.print_time()   # Use public methods
race.print_pace()   # Don't call _diff_time()
```

---

## Using the RaceTime Class

Programmers only call public methods:

```python
race = RaceTime(9, 30, 10, 3, 5.0)

# Use PUBLIC interface
race.print_time()   # User-friendly
race.print_pace()   # User-friendly

# Private method exists but shouldn't be called
# (though Python allows it)
# result = race._diff_time()  # Discouraged!
```

---

## Why Public/Private Matters

**Advantages:**

1. **Clarity:** Shows what methods users should call
2. **Flexibility:** Can change internal methods without affecting users
3. **Simplicity:** Users don't need to understand internal details

```python
# Without clear interface - confusing!
race = RaceTime(9, 30, 10, 3, 5.0)
time = race._diff_time()        # Is this for me to use?
hours, mins = time              # How do I use this?
result = race.print_time()      # What does this return?

# With clear interface - obvious!
race.print_time()               # Clear: print the time
```

---

## Abstract Data Types (ADT)

**ADT:** A data type with specific, well-defined operations

The interface IS the ADT!

```python
# RaceTime is an ADT with:
# - Creation: __init__(start_hrs, start_mins, end_hrs, end_mins, dist)
# - Operations: print_time(), print_pace()
# - Implementation: hidden (uses _diff_time() internally)

# User only cares about the interface, not how it works
race = RaceTime(5, 30, 7, 0, 5.0)
race.print_time()
race.print_pace()
```

---

## Information Hiding

**Information hiding:** Hide internal implementation

Users see only the interface:

```
┌─────────────────────────────────────┐
│  CLASS INTERFACE (Public)           │
│  - __init__()                       │
│  - print_time()                     │
│  - print_pace()                     │
└─────────────────────────────────────┘
        │
        │ User calls these
        │
┌─────────────────────────────────────┐
│  INTERNAL IMPLEMENTATION (Private)  │
│  - _diff_time()                     │
│  - Internal attributes              │
│  - Calculation details              │
└─────────────────────────────────────┘
```

---

## Benefits of Information Hiding

**For users:**

- Simpler to use (fewer methods to learn)
- Don't need to understand internals
- More productive

**For developers:**

- Can improve internal code without breaking users' code
- Can change `_diff_time()` implementation anytime

```python
# Old internal implementation
def _diff_time(self):
    # Long calculation...
    return (hours, minutes)

# New internal implementation (better)
def _diff_time(self):
    # More efficient calculation...
    return (hours, minutes)

# Users' code still works!
race.print_time()  # Unaffected by change
```

---

## Python's Approach to Privacy

**Python is "trusting"**

- No true `private` keyword
- Underscore is just a convention
- Python won't prevent access

```python
# This is allowed (but discouraged)
race = RaceTime(5, 30, 7, 0, 5.0)
internal_result = race._diff_time()  # Python allows it!

# Underscore says: "I'm private, don't use me"
# But Python can't enforce it
```

---

## Privacy in Other Languages

**Java and C++ enforce privacy:**

```
private def _diff_time():  # Truly private
    # Raises error if accessed from outside
```

**Python is different:**

- Relies on programmer convention
- Trusts you to respect `_underscore` prefix
- More flexible, but requires discipline

---

## Best Practice: Clear Interface

**Good design = clear interface**

```python
class Student:
    def __init__(self, name):
        self._grades = []  # Private!

    # PUBLIC interface - use these!
    def add_grade(self, grade):
        self._grades.append(grade)

    def get_average(self):
        return sum(self._grades) / len(self._grades)

    def display_grades(self):
        print(self._grades)
```

---

## Using Clear Interface

```python
# User knows to call:
alice = Student("Alice")
alice.add_grade(95)
alice.add_grade(88)
alice.get_average()      # 91.5
alice.display_grades()

# User shouldn't access:
# alice._grades = []  # Discouraged! But Python allows it
```

---

## Real Example: BankAccount ADT

```python
class BankAccount:
    """ADT for managing bank accounts"""

    def __init__(self, owner, initial_balance=0):
        self._owner = owner
        self._balance = initial_balance
        self._transaction_count = 0

    def deposit(self, amount):
        self._balance += amount
        self._transaction_count += 1
        return self._balance

    def withdraw(self, amount):
        if amount <= self._balance:
            self._balance -= amount
            self._transaction_count += 1
            return True
        return False
```

---

## BankAccount Public Interface

```python
    def get_balance(self):
        return self._balance

# Private attributes: _owner, _balance, _transaction_count
# Public interface: deposit(), withdraw(), get_balance()
```

---

## Using BankAccount ADT

```python
account = BankAccount("Alice", 500)

# PUBLIC interface
account.deposit(100)
account.withdraw(50)
print(account.get_balance())

# Users don't care about:
# - How _balance is stored
# - How _transaction_count works
# - Internal implementation details

# What matters: methods work correctly!
```

---

## Good Interface Design

**Small, focused interface:**

```python
class Timer:
    def start(self):
        pass

    def stop(self):
        pass

    def get_elapsed(self):
        pass

# Simple, clear, easy to use
timer = Timer()
timer.start()
timer.stop()
elapsed = timer.get_elapsed()
```

---

## Confusing Interface Design

**Too many public methods:**

```python
class BadTimer:
    def start_internal_mechanism(self):
        pass

    def get_milliseconds_since_epoch(self):
        pass

    def calculate_elapsed(self):
        pass

    def update_timer(self):
        pass
    # ... many more confusing methods
```

Users don't know what to call!

---

## Summary: Class Interfaces

**Public vs Private:**

- Public methods: Users interact with these
- Private methods (prefix `_`): Internal use only
- Clear interface = happy users

**Information Hiding:**

- Hide complexity of implementation
- Show only what matters
- Makes code easier to use and maintain

**Key Concept: Abstract Data Types (ADT)**

- User asks: "What can I do?"
- Developer asks: "How do I do it?"
- Interface separates the two

---

## Conclusion: Object-Oriented Programming

**What we've learned:**

- Classes organize data and functions together
- Objects make code clearer and more reusable
- Methods group related operations
- Interfaces hide internal complexity
- Well-designed classes feel natural to use

**These are the foundations of OOP!**

Next lecture: We'll explore more ways to customize objects and their behavior.

---

## Summary: Why Use OOP?

**Benefits of Object-Oriented Programming:**

- **Organization:** Related data and functions grouped
- **Reusability:** Create many instances from one class
- **Clarity:** Code shows what objects do
- **Maintainability:** Changes in one place affect all uses
- **Flexibility:** Can improve internals without breaking users' code
- **Natural syntax:** Objects work like built-in types
