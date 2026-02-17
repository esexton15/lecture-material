---
marp: true
theme: gaia
class: invert
paginate: true
---

<style>
h1 {
	font-size: 2.5em;
	height: 100%;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
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

# Reading and Writing Files

---

# Part 1 - Reading Files

---

## Opening and Reading Files

The `open()` function creates a file object for reading or writing.

```python
f = open("myfile.txt")  # create file object
contents = f.read()      # read entire file as string
f.close()                # close the file
```

**Key points:**

- `open()` returns a file object
- File must exist to open for reading
- Path can be relative or absolute
- Always call `close()` when done

---

## Read Methods

**file.read()** - Returns entire file contents as a string

```python
f = open("myfile.txt")
contents = f.read()
f.close()
print(contents)
```

**file.readlines()** - Returns list of strings (one per line)

```python
f = open("myfile.txt")
lines = f.readlines()
f.close()
# lines = ['Line 1\n', 'Line 2\n', 'Line 3\n']
```

---

## Read Methods (continued)

**file.readline()** - Returns a single line at a time

Useful for large files that won't fit in memory:

```python
f = open("myfile.txt")
line1 = f.readline()  # gets first line
line2 = f.readline()  # gets second line
f.close()
```

All methods detect EOF (end-of-file) automatically and stop reading.

---

## Processing Data from a File

Common task: read file, process each line, compute result

```python
# Read file
f = open("mydata.txt")
lines = f.readlines()
f.close()

# Process each line
total = 0
for ln in lines:
    total += int(ln)

# Compute result
avg = total / len(lines)
print(f"Average: {avg}")
```

---

## Iterating Over File Lines

Files support iteration directly with `for ... in` syntax:

```python
f = open("myfile.txt")

for line in f:
    print(line, end="")

f.close()
```

This is efficient for large files—reads one line at a time rather than loading entire file into memory.

---

# Part 2 - Writing Files

---

## Writing Files

Open with mode `"w"` and use `write()` to add strings:

```python
f = open("myfile.txt", "w")      # open for writing
f.write("Example string:\n")
f.close()
```

- `write()` accepts strings only
- Overwrites existing file contents
- Use `f.close()` when done

---

## Converting Values to Strings

`write()` only accepts strings. Convert numbers using `str()`:

```python
num1 = 5
num2 = 7.5
num3 = num1 + num2

f = open("myfile.txt", "w")
f.write(str(num1))
f.write(" + ")
f.write(str(num2))
f.write(" = ")
f.write(str(num3))
f.close()
```

Output: `5 + 7.5 = 12.5`

---

## File Modes

The second argument to `open()` specifies the mode:

| Mode   | Purpose    | Read | Write | Create | Overwrite |
| ------ | ---------- | ---- | ----- | ------ | --------- |
| `"r"`  | Read       | ✓    |       |        |           |
| `"w"`  | Write      |      | ✓     | ✓      | ✓         |
| `"a"`  | Append     |      | ✓     | ✓      |           |
| `"r+"` | Read/Write | ✓    | ✓     |        |           |
| `"w+"` | Read/Write | ✓    | ✓     | ✓      | ✓         |

---

## Output Buffering

Data written to a file is buffered before being written to disk.

By default: **line-buffered** (writes when newline is output)

May be delay between `write()` and actual disk write.

Control buffer size with `buffering` parameter:

```python
f = open("myfile.txt", "w", buffering=100)  # 100 byte buffer
f = open("myfile.txt", "w", buffering=1)    # line-buffered (default)
```

---

## Flushing the Buffer

Force write to disk with `flush()`:

```python
f = open("myfile.txt", "w")
f.write("Write me!")
f.flush()              # forces write to disk immediately
```

Useful when you need data saved before continuing.

---

# Part 3 - Interacting with File Systems

---

## Portability Issues

File paths differ across operating systems:

- **Windows:** `"subdir\\bat_mobile.jpg"` (backslash separator)
- **Mac/Linux:** `"subdir/bat_mobile.jpg"` (forward slash separator)

Hardcoding paths reduces **portability**—programs may fail on different OS.

Solution: Use `os.path` module functions to build paths correctly for any OS.

---

## os.path.join()

`os.path.join()` builds paths using the correct separator for the current OS:

```python
import os

# Portable path building
file_path = os.path.join("logs", "1997", "8", "29", "log.txt")

# Windows: logs\1997\8\29\log.txt
# Mac/Linux: logs/1997/8/29/log.txt
```

Always use `os.path.join()` instead of hardcoding separators.

---

## Path Utilities

**os.path.split(path)** - Split into (head, tail)

```python
p = os.path.join("C:\\", "Users", "BWayne", "batsuit.jpg")
print(os.path.split(p))  # ('C:\\Users\\BWayne', 'batsuit.jpg')
```

**os.path.sep** - Path separator for current OS (`\\` or `/`)

```python
tokens = path.split(os.path.sep)  # Split path into tokens
```

---

## Checking Paths

**os.path.exists(path)** - Does path exist?

```python
if os.path.exists("myfile.txt"):
    print("File found!")
```

**os.path.isfile(path)** - Is path a file (not directory)?

```python
if os.path.isfile(p):
    print("It's a file!")
else:
    print("Not a file (maybe directory?)")
```

---

## File Information

**os.path.getsize(path)** - Get file size in bytes

```python
import os
p = os.path.join("data", "image.jpg")
size = os.path.getsize(p)
print(f"File size: {size} bytes")
```

Useful for checking file properties before processing.

---

## Walking Directory Trees

`os.walk()` recursively traverses a directory structure:

```python
for dirname, subdirs, files in os.walk("logs"):
    # Process directory...
```

Returns three-tuple per iteration:

- `dirname`: current directory path
- `subdirs`: list of subdirectories
- `files`: list of files in directory

---

## os.walk() Example

Directory structure:

```
logs/
  2009/
    April/
      1/
        log.txt
        words.doc
    January/
      15/
        log.txt
```

---

## os.walk() Output

Walking it:

```python
for dirname, subdirs, files in os.walk("logs/2009"):
    print(dirname, subdirs, files)
```

Output:

```
logs/2009 ['April', 'January'] []
logs/2009/April ['1'] []
logs/2009/April/1 [] ['log.txt', 'words.doc']
```

Each line is (current dir, subdirs, files)

---

## Use Cases for os.walk()

**Search for files matching pattern:**

```python
for dirname, subdirs, files in os.walk("data"):
    for file in files:
        if file.endswith(".txt"):
            full_path = os.path.join(dirname, file)
            print(f"Found: {full_path}")
```

**Filter by file extension:**

```python
for dirname, subdirs, files in os.walk("downloads"):
    for file in files:
        if file.endswith(".pdf"):
            process_pdf(file)
```

---

# Part 4 - Binary Data

---

## Binary Data Basics

**Binary data** - sequence of bytes not encoded as text (images, videos, PDFs)

Create bytes objects:

```python
my_bytes = b"Hello"                    # bytes literal
my_bytes = bytes([65, 66, 67])         # from list
```

Bytes are **immutable** (like strings).

---

## Bytes Literals and Escape Sequences

Use `b"..."` prefix for bytes literals:

```python
my_bytes = b"This is a bytes literal"
print(my_bytes)
# b'This is a bytes literal'
```

Specify raw byte values with `\x` and hexadecimal:

```python
print(b"\x31\x32\x33\x34\x35")  # 1-5 in hex
# b'12345'
```

Each `\xHH` is a single byte (0-255 in decimal).

---

## Binary File Mode

Open with `"b"` in mode string: `"rb"`, `"wb"`

```python
f = open("image.bmp", "rb")
contents = f.read()      # returns bytes object
f.close()
```

Key differences:

- `read()` returns `bytes` instead of `str`
- `write()` expects `bytes` argument

---

## Inspecting Binary Contents

Binary files often have a **header** describing the file format:

```python
f = open("ball.bmp", "rb")
contents = f.read()
f.close()

print(contents[:20])  # first 20 bytes
# b'BM\xb4\x06\x00\x00\x00\x00\x006\x04\x00\x00...'
```

BMP header example:

- First 2 bytes: `"BM"` (file type)
- Next 4 bytes: file size
- Position of pixel data

---

## Altering Binary Files

<!-- Example: read a BMP image, modify pixel data, write new file -->

```python
import struct

# Read image
f = open("ball.bmp", "rb")
ball_data = f.read()
f.close()

# Find pixel location (bytes 10-14)
pixel_loc = struct.unpack("<L", ball_data[10:14])[0]

# Create new pixels (red, green, yellow)
new_pixels = b"\x01"*3000 + b"\x02"*3000 + b"\x03"*3000

# Replace pixels in data
new_data = ball_data[:pixel_loc] + new_pixels + ball_data[pixel_loc + len(new_pixels):]

# Write new file
f = open("new_ball.bmp", "wb")
f.write(new_data)
f.close()
```

---

## Packing Values into Bytes

```python
import struct
struct.pack(">h", 5)        # b'\x00\x05'
struct.pack(">h", 256)      # b'\x01\x00'
struct.pack(">hh", 5, 256)  # b'\x00\x05\x01\x00'
```

Format string components:

- `">"` = big-endian (most significant byte first)
- `"<"` = little-endian (least significant byte first)
- `"h"` = 2-byte integer
- `"b"` = 1-byte integer, `"I"` = 4-byte integer, `"s"` = string

---

## Unpacking Bytes

`struct.unpack()` converts bytes back into values:

```python
import struct

struct.unpack(">h", b"\x00\x05")           # (5,)
struct.unpack(">h", b"\x01\x00")           # (256,)
struct.unpack(">hh", b"\x00\x05\x01\x00")  # (5, 256)
```

Returns a **tuple** with results (even for single value).

```python
value = struct.unpack(">h", b"\x00\x05")[0]  # extract first value
```

---

# Part 5 - Command-Line Arguments and Files

---

## Using Command-Line Arguments

Programs can accept input file names via command-line arguments:

```bash
python my_script.py myfile.txt
```

Access arguments in code using `sys.argv`:

```python
import sys

print(sys.argv)
# ['my_script.py', 'myfile.txt']

# sys.argv[0] = script name
# sys.argv[1] = first argument
# sys.argv[2] = second argument, etc.
```

---

## Validating Arguments

Check that the correct number of arguments were provided:

```python
import sys

if len(sys.argv) != 2:
    print(f"Usage: {sys.argv[0]} input_file")
    sys.exit(1)  # exit with error code 1

print(f"Processing file: {sys.argv[1]}")
```

**sys.exit(code):**

- Exit code 0 = success
- Exit code 1 = error

---

## Checking File Existence

Always verify a file exists before opening:

```python
import sys
import os

filename = sys.argv[1]

if not os.path.exists(filename):
    print(f"Error: {filename} does not exist.")
    sys.exit(1)

f = open(filename, "r")
# proceed with file operations
```

---

## Complete Example

Read two integers from a file specified on command line:

```python
import sys
import os

if len(sys.argv) != 2:
    print(f"Usage: {sys.argv[0]} input_file")
    sys.exit(1)

if not os.path.exists(sys.argv[1]):
    print(f"Error: {sys.argv[1]} does not exist.")
    sys.exit(1)

f = open(sys.argv[1], "r")
num1 = int(f.readline())
num2 = int(f.readline())
f.close()

print(f"Sum: {num1 + num2}")
```

---

## Running with Different Inputs

**Success case:**

```bash
$ python script.py myfile.txt
Sum: 15
```

**Missing argument:**

```bash
$ python script.py
Usage: script.py input_file
```

**File not found:**

```bash
$ python script.py missing.txt
Error: missing.txt does not exist.
```

---

# Part 6 - The with Statement

---

## Automatic File Closing

The `with` statement automatically closes a file when done:

```python
with open("myfile.txt", "r") as f:
    contents = f.read()
    # process contents

# f automatically closed here
```

No need to call `f.close()` explicitly.

---

## Why Use with?

**Without with** - manual close required:

```python
f = open("myfile.txt", "r")
contents = f.read()
f.close()  # Easy to forget!
```

**Problems if file not closed:**

- Other programs can't write to file
- File handle remains open (resource leak)
- May cause file system issues

---

## with Statement Benefits

```python
with open("myfile.txt", "r") as f:
    num1 = int(f.readline())
    num2 = int(f.readline())

# File automatically closed here

print(f"Sum: {num1 + num2}")
```

**Advantages:**

- File guaranteed to close (even on error)
- Cleaner code
- Less error-prone
- Best practice in Python

---

## Context Managers

The `with` statement creates a **context manager**:

- Performs setup (opens file)
- Executes code block
- Performs teardown (closes file)

Works with any resource that needs setup/cleanup, not just files.

---

## Recommendation

**Always use `with` when opening files:**

```python
# Good: uses with statement
with open("data.txt", "r") as f:
    data = f.read()

# Avoid: manual close
f = open("data.txt", "r")
data = f.read()
f.close()
```

---

# Part 7 - Comma-Separated Values Files

---

## CSV Format

**CSV (Comma-Separated Values)** - text format for tabular data:

```
name,hw1,hw2,midterm,final
Petr Little,9,8,85,78
Sam Tarley,10,10,99,100
Joff King,4,2,55,61
```

Rows = lines, columns = comma-separated fields.

Perfect for exam scores, data records, exports from spreadsheets.

---

## Reading CSV Files

```python
import csv

with open("grades.csv", "r") as csvfile:
    grades_reader = csv.reader(csvfile, delimiter=",")

    for row in grades_reader:
        print(row)
```

Output:

```
['name', 'hw1', 'hw2', 'midterm', 'final']
['Petr Little', '9', '8', '85', '78']
['Sam Tarley', '10', '10', '99', '100']
```

---

## CSV Reader Details

**csv.reader(file, delimiter=",")**

- `delimiter`: character separating fields (default: comma)
- Returns iterable of rows (each row is a list)
- All values are strings

```python
for row in grades_reader:
    name = row[0]           # string
    hw1 = row[1]            # string
    midterm = int(row[3])   # convert to int
```

---

## Processing CSV Data

```python
import csv

grades = {}

with open("grades.csv", "r") as csvfile:
    reader = csv.reader(csvfile)

    first_row = True
    for row in reader:
        if first_row:
            first_row = False
            continue

        name = row[0]
        scores = [float(x) for x in row[1:]]

        # Calculate weighted score
        final = (scores[0]/10 * 0.05 +
                scores[2]/100 * 0.40 +
                scores[3]/100 * 0.50) * 100

        grades[name] = final

for student, score in grades.items():
    print(f"{student}: {score:.1f}%")
```

---

## Writing CSV Files

Use `csv.writer()` to write rows:

```python
import csv

row1 = ["100", "50", "29"]
row2 = ["76", "32", "330"]

with open("output.csv", "w", newline="") as csvfile:
    writer = csv.writer(csvfile)

    writer.writerow(row1)   # write single row
    writer.writerow(row2)

    writer.writerows([row1, row2])  # write multiple rows
```

Output file:

```
100,50,29
76,32,330
100,50,29
76,32,330
```

**Note:** `newline=""` required on Windows for proper line handling.

---

## CSV Writer Details

**csv.writer(file, delimiter=",")**

- `writerow(list)`: write one row
- `writerows(list_of_lists)`: write multiple rows
- Values converted to strings automatically
- Handles commas in fields automatically (uses quotes)

```python
data = [["Smith, John", "100"], ["Doe, Jane", "95"]]
writer.writerows(data)
# Output: "Smith, John",100
#         "Doe, Jane",95
```
