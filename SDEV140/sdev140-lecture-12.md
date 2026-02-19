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

# Building Robust & Secure Programs

Professional Development Practices

---

# Part 1 - The Development Process

---

## Why Professional Practices Matter

**Bad code costs money:**

- Security breaches
- Lost data
- Customer trust
- Developer time fixing bugs

**Good practices save:**

- Development time
- Debugging effort
- Security incidents
- Maintenance costs

---

## The Software Development Lifecycle (SDLC)

1. **Planning** - Understand the problem
2. **Requirements** - What does the user need?
3. **Design** - Plan the solution (algorithms)
4. **Implementation** - Write the code
5. **Testing** - Does it work correctly?
6. **Deployment** - Put it into production
7. **Maintenance** - Fix bugs, add features

Each phase has specific goals and outputs.

---

## Today's Case Study

**Problem:** Build a Student Grade Tracker

**User Story:**
"As a teacher, I need to track student grades for multiple assignments, calculate averages, and identify students who need help."

We'll build this together using professional practices.

---

# Part 2 - Problem Analysis & Requirements

---

## Understanding the Real Problem

**Ask questions:**

- Who will use this?
- What do they need to accomplish?
- What are the constraints?
- What could go wrong?

**For our grade tracker:**

- Teachers use it daily
- Need to add/update grades quickly
- Must be accurate
- Data cannot be lost
- Privacy is critical

---

## Gathering Requirements

**Functional:**

- Add students
- Record grades
- Calculate averages
- Find struggling students
- Save/load data

**Non-Functional:**

- Validate all input
- Handle errors gracefully
- Protect student data

---

## Identifying Edge Cases

What could break our program?

**Invalid inputs:**

- Negative grades / grades over 100
- Empty or invalid student names
- Missing data

**System issues:**

- File doesn't exist or is corrupted
- No write permissions

---

# Part 3 - Algorithm Design

---

## Breaking Down the Problem

Divide into smaller functions:

1. `add_student(students, name)` - Add student
2. `add_grade(students, name, grade)` - Record grade
3. `calculate_average(students, name)` - Compute average
4. `find_struggling(students, threshold)` - Find at-risk students
5. `save_data(students, filename)` - Save to file
6. `load_data(filename)` - Load from file

---

## Pseudocode: Add Student

```
FUNCTION add_student(name):
    IF name is empty OR name is only whitespace:
        RETURN error "Name cannot be empty"

    IF name contains invalid characters:
        RETURN error "Name contains invalid characters"

    IF student already exists:
        RETURN error "Student already exists"

    CREATE new student record
    INITIALIZE empty grade list
    RETURN success
```

Think through logic before coding.

---

## Pseudocode: Add Grade

```
FUNCTION add_grade(student, assignment, grade):
    IF student does not exist:
        RETURN error "Student not found"

    IF grade < 0 OR grade > 100:
        RETURN error "Grade must be between 0 and 100"

    IF assignment name is empty:
        RETURN error "Assignment name required"

    ADD grade to student's record
    RETURN success
```

Validate every input!

---

## Algorithm Design Benefits

**Why design first?**

- Catch logic errors early
- Plan for edge cases
- Easier to review
- Language-independent
- Can estimate complexity

**Design saves time** - fixing a design flaw is cheaper than fixing code.

---

# Part 4 - Defensive Programming

---

## What is Defensive Programming?

**Assume everything will fail:**

- User input is wrong
- Files don't exist
- Network is down
- Memory is full

**Write code that:**

- Validates all inputs
- Handles all errors
- Fails gracefully
- Logs problems

---

## Input Validation

**Never trust user input:**

```python
# BAD: No validation
def add_grade(students, name, grade):
    students[name].append(grade)
```

```python
# GOOD: Validate everything
def add_grade(students, name, grade):
    if not name or not name.strip():
        raise ValueError("Name cannot be empty")
    if not isinstance(grade, (int, float)):
        raise TypeError("Grade must be a number")
    if grade < 0 or grade > 100:
        raise ValueError("Grade must be 0-100")
    students[name].append(grade)
```

---

## Type Checking

Validate types and values:

```python
def calculate_average(grades):
    if not isinstance(grades, list):
        raise TypeError("Grades must be a list")
    if len(grades) == 0:
        raise ValueError("Cannot average empty list")
    for grade in grades:
        if not isinstance(grade, (int, float)):
            raise TypeError(f"Invalid grade: {grade}")
    return sum(grades) / len(grades)
```

---

## Error Handling

**Use try/except for external operations:**

```python
def load_grades(filename):
    try:
        with open(filename, "r") as f:
            data = json.load(f)
            return data
    except FileNotFoundError:
        print(f"Error: {filename} not found")
        return {}
    except json.JSONDecodeError:
        print(f"Error: {filename} is corrupted")
        return {}
    except PermissionError:
        print(f"Error: No permission to read {filename}")
        return {}
```

Handle specific errors differently.

---

## Fail-Safe Defaults

**Provide sensible defaults:**

```python
def get_average(students, name, default=0):
    if name not in students or not students[name]:
        return default
    return sum(students[name]) / len(students[name])

def save_grades(students, filename="grades.json"):
    try:
        with open(filename, "w") as f:
            json.dump(students, f)
    except Exception as e:
        print(f"Warning: Could not save: {e}")
```

---

## Assertions for Development

Catch programming errors:

```python
def calculate_weighted_average(grades, weights):
    assert len(grades) == len(weights), "Length mismatch"
    assert sum(weights) == 1.0, "Weights must sum to 1.0"
    return sum(g * w for g, w in zip(grades, weights))
```

**Use for:** Logic errors, not user input
**Example:** Checking function preconditions

---

# Part 5 - Documentation Standards

---

## Why Documentation Matters

**Code is read more than written:**

- You'll forget what it does
- Others need to maintain it
- Users need to use it

**Good documentation:**

- Explains the "why"
- Describes parameters
- Notes edge cases
- Provides examples

---

## Docstrings (PEP 257)

Document every function:

```python
def calculate_average(grades):
    """
    Calculate average of grade list.

    Args:
        grades: List of numeric grades (0-100)

    Returns:
        Average grade as float

    Raises:
        ValueError: If grades list is empty
        raise ValueError("Cannot average empty list")
    return sum(grades) / len(grades)
```

---

## Module-Level Documentation

Every file should explain its purpose:

```python
"""
Student Grade Tracker

Provides functions for tracking student grades and
calculating averages.

Functions:
    add_student: Add new student
    add_grade: Record a grade
    calculate_average: Compute average
    load_grades: Load from JSON
    save_grades: Save to JSON

Author: Your Name
Date: 2026
"""
```

---

## README Files

Every project needs a README:

```markdown
# Student Grade Tracker

## Description

Track student grades and calculate statistics.

## Installation

pip install -r requirements.txt

## Usage

python grade_tracker.py --file grades.json

## Requirements

- Python 3.8+
- json module (built-in)

## License

MIT License
```

---

# Part 6 - Security Considerations

---

## Security in the Application Layer

**Attackers target applications:**

- 75% of cyber attacks are at the application layer
- Exploits programming mistakes
- Takes advantage of poor validation

**Common vulnerabilities:**

- Invalid input handling
- Weak error handling
- Insecure file access
- Poor data validation

---

## Secure File Handling

**Validate file paths:**

```python
import os

def load_grades(filename):
    # BAD: User could input "../../etc/passwd"
    with open(filename, "r") as f:
        return json.load(f)

    # GOOD: Validate path
    base_dir = "/var/app/data"
    abs_path = os.path.abspath(filename)

    if not abs_path.startswith(base_dir):
        raise ValueError("Invalid file path")

    with open(abs_path, "r") as f:
        return json.load(f)
```

Prevent directory traversal attacks.

---

## Principle of Least Privilege

**Grant minimum necessary permissions:**

```python
# BAD: Run with admin privileges
# All operations have full system access

# GOOD: Drop privileges after initialization
import os

# Start as root to bind port 80
start_server(port=80)

# Drop to normal user
os.setuid(1000)  # Switch to non-privileged user

# Now application runs with limited permissions
```

---

# Part 7 - Secure Development Lifecycle

---

## What is Secure SDLC?

**Integrate security at every phase:**

1. **Planning** - Identify security requirements
2. **Requirements** - Define security features
3. **Design** - Plan security architecture
4. **Implementation** - Follow secure coding practices
5. **Testing** - Security testing & pen testing
6. **Deployment** - Secure configuration
7. **Maintenance** - Security patches & updates

Security is not an afterthought!

---

## Security in Planning Phase

**Identify threats early:**

- What data needs protection?
- Who are potential attackers?
- What are attack vectors?
- What regulations apply? (FERPA for student data)

**For our grade tracker:**

- Protect student privacy (FERPA)
- Prevent grade tampering
- Ensure data integrity
- Limit access to authorized users

---

## Security in Design Phase

**Design with security in mind:**

- Use principle of least privilege
- Design secure data flow
- Consider input validation
- Plan error handling
- Protect file access

---

## Security in Design Phase - Example:

```
[User] -> [Grade Input]
            |
            v
      [Validate Input]
            |
            v
      [Check Permissions]
            |
            v
         [Save]
```

---

## Security in Implementation Phase

**Follow secure coding practices:**

- Validate all inputs
- Never hardcode sensitive values
- Use proper file permissions
- Handle errors securely
- Log security-relevant events

---

## Security in Implementation Phase - Example

```python
# BAD: Hardcoded configuration
DATA_FILE = "/Users/teacher/grades.json"

# GOOD: Environment variable
import os
DATA_FILE = os.environ.get("DATA_FILE", "grades.json")
if not DATA_FILE:
    raise RuntimeError("DATA_FILE not set")
```

---

## Security Testing

**Test for security vulnerabilities:**

- **Input validation testing** - Try malicious inputs
- **Boundary testing** - Test limits
- **Error handling** - Ensure errors don't leak info
- **Penetration testing** - Simulate attacks
- **Code review** - Have others review

---

## Security Testing - Example

```python
# Test with malicious inputs
test_cases = [
    "",                    # Empty
    " ",                   # Whitespace only
    "../../../etc/passwd", # Path traversal
    "123",                 # Numbers only
    "!@#$%",              # Special characters
    "A" * 10000,          # Very long input
]

for test in test_cases:
    try:
        add_student(test)
        print(f"FAIL: Accepted invalid input: {test}")
    except ValueError:
        print(f"PASS: Rejected: {test}")
```

---

## Deployment Security

**Secure the production environment:**

- Set proper file permissions
- Disable debug mode
- Use environment variables for configuration
- Keep software updated
- Monitor logs for suspicious activity

```python
# BAD: Debug mode in production
DEBUG = True  # Exposes stack traces!

# GOOD: Check environment
import os
DEBUG = os.environ.get("ENV") == "development"
```

---

## Maintenance & Updates

**Security is ongoing:**

- Monitor for vulnerabilities (CVEs)
- Apply security patches promptly
- Review logs regularly
- Update dependencies
- Retire old systems

**Example workflow:**

1. Security bulletin released
2. Assess impact on your application
3. Test patch in dev environment
4. Deploy to production quickly
5. Verify fix works

---

# Part 8 - Putting It All Together

---

## Complete Example: Grade Tracker

```python
"""
Student Grade Tracker - Secure Implementation
Demonstrates professional development practices
"""

import json
import os

# Global data structure: {student_name: [grade1, grade2, ...]}
students = {}
```

---

## Load Data Function

```python
def load_grades(filename):
    """
    Load grades from JSON file.

    Returns:
        Dictionary of {student: [grades]}
    """
    # Prevent directory traversal
    if ".." in filename:
        raise ValueError("Invalid file path")

    try:
        if os.path.exists(filename):
            with open(filename, "r") as f:
                return json.load(f)
        return {}
    except json.JSONDecodeError:
        print(f"Error: Corrupted file {filename}")
        return {}
    except PermissionError:
        print(f"Error: No permission to read {filename}")
        raise
```

---

## Add Student Function

```python
def add_student(students, name):
    """
    Add student to grade tracker.

    Args:
        students: Grade dictionary
        name: Student's full name

    Raises:
        ValueError: If name is invalid
    """
    # Validate name
    if not name or not name.strip():
        raise ValueError("Name cannot be empty")

    name = name.strip()
    if not name.replace(" ", "").replace("-", "").isalpha():
        raise ValueError("Name has invalid characters")

    # Check if exists
    if name in students:
        return False

    students[name] = []
    return True
```

---

## Add Grade Function

```python
def add_grade(students, name, grade):
    """
    Add a grade for a student.

    Args:
        students: Grade dictionary
        name: Student name
        grade: Grade value (0-100)

    Raises:
        ValueError: If invalid
    """
    if name not in students:
        raise ValueError(f"Student not found: {name}")

    if not isinstance(grade, (int, float)):
        raise TypeError("Grade must be a number")

    if grade < 0 or grade > 100:
        raise ValueError("Grade must be 0-100")

    students[name].append(float(grade))
    return True
```

---

## Calculate & Find Functions

```python
def calculate_average(students, name):
    """Calculate student's average grade."""
    if name not in students:
        raise ValueError(f"Student not found: {name}")

    grades = students[name]
    if not grades:
        return None
    return sum(grades) / len(grades)

def find_struggling_students(students, threshold=60.0):
    """Find students below threshold."""
    struggling = []
    for name in students:
        avg = calculate_average(students, name)
        if avg is not None and avg < threshold:
            struggling.append(name)
    return struggling
```

---

## Save Function & Usage

```python
def save_grades(students, filename):
    """Save grades with secure permissions."""
    try:
        with open(filename, "w") as f:
            json.dump(students, f, indent=2)
        os.chmod(filename, 0o600)  # Owner only
        print("Grades saved successfully")
    except Exception as e:
        print(f"Error: Could not save: {e}")
        raise
```

---

## Example Usage

```python
# Example usage
students = load_grades("grades.json")

print("Enter student name:")
student = input("> ")
print("Enter grade:")
grade = input("> ")
try:
	grade = float(grade)
except Exception as e:
	print(f"Invalid grade: {e}")
	exit(1)

add_student(students, student)
add_grade(students, student, grade)

avg = calculate_average(students, student)
print(f"{student}: {avg:.1f}")

struggling = find_struggling_students(students, 60)
print(f"Needs help: {struggling}")

save_grades(students, "grades.json")
```

---

## Code Review Checklist

**Before committing code:**

✓ Input validation on all user input
✓ Error handling for external operations  
✓ Docstrings on all functions
✓ Type hints where helpful
✓ No hardcoded secrets
✓ Proper file permissions
✓ Logging for important events
✓ No sensitive data in logs
✓ Tests for edge cases
✓ Security considerations addressed

---

## Key Takeaways

**Professional development means:**

1. **Plan before coding** - Requirements, design, algorithm
2. **Validate everything** - Never trust input
3. **Handle errors gracefully** - Fail safely
4. **Document thoroughly** - Future you will thank you
5. **Think security first** - Protect users and data
6. **Test extensively** - Including malicious inputs
7. **Review and iterate** - Code improves with review

---

## Industry Standards Summary

**Follow established practices:**

- **PEP 8** - Python style guide
- **PEP 257** - Docstring conventions
- **OWASP Top 10** - Common security vulnerabilities
- **Semantic Versioning** - Version numbering
- **Git workflow** - Version control practices

**Resources:**

- python.org/dev/peps
- owasp.org
- cwe.mitre.org (Common Weakness Enumeration)

---

## Final Thoughts

**Good code is:**

- Correct (meets requirements)
- Robust (handles errors)
- Secure (protects data)
- Maintainable (documented)
- Efficient (reasonable performance)
