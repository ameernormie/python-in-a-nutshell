# Python in a Nutshell

---

Table of Contents

- [1 Python Interpreter](#python-interpreter)
- [2 Core Python Language and Build-ins](#core-python-language-and-built-ins)
  - [2.1 Lexical Structure](#lexical-structure)
    - [2.1.1 Tokens](#tokens)
    - [2.1.2 Identifiers](#identifiers)
    - [2.1.3 Keywords](#keywords)
    - [2.1.4 Operators](#operators)
    - [2.1.5 Delimiters](#delimiters)
    - [2.1.6 Statements](#statements)
  - [2.2 Data Types](#data-types)
    - [2.2.1 Numbers](#numbers)
    - [2.2.2 Integer Numbers](#integer-numbers)
    - [2.2.3 Floating point numbers](#floating-point-numbers)
    - [2.2.4 Complex Numbers](#complex-numbers)
    - [2.2.5 Underscores in Numeric Literals](#underscores-in-numeric-literals)
    - [2.2.6 Sequences](#sequences)
    - [2.2.7 Iterables](#iterables)
    - [2.2.8 Strings](#strings)
    - [2.2.9 Tuples](#tuples)
    - [2.2.10 Sets](#sets)
    - [2.2.11 Dictionaries](#dictionaries)
    - [2.2.12 None](#none)
    - [2.2.12 Callables](#callables)
    - [2.2.13 Boolean Values](#boolean-values)
  - [2.3 Variables and Other References](#variables-and-other-references)
    - [2.3.1 Variables](#variables)
      - [2.3.1.1 Object Attributes and Items](#object-attributes-and-items)
      - [2.3.1.2 Accessing nonexistent references](#accessing-nonexistent-references)
    - [2.3.2 Assignment Statements](#assignment-statements)
      - [2.3.2.1 Plain Assignment](#plain-assignment)
      - [2.3.2.2 Augmented Assignment](#augmented-assignment)
      - [2.3.2.3 Del Statements](#del-statements)

## Python Interpreter

Python frequently used command-line options:

- `-B` - Don’t save compiled bytecode files to disk (PYTHONDONTWRITEBYTECODE)
- `-c` - Specifies Python statements as part of the command line
- `-E` - Ignores all environment variables
- `-h` - Prints a full list of options and summary help, then terminates
- `-i` - Runs an interactive session after the file or command runs (PYTHONINSPECT)
- `-m` - Specifies a Python module or package to run as the main script
- `-O` - Optimizes generated bytecode (PYTHONOPTIMIZE)—note that this is an uppercase letter O, not the digit0
- `-OO` - Like -O, but also removes documentation strings from the bytecode
- `--Q arg` - Controls the behavior of division operator / on integers (v2 only)
- `-S` - Omits the implicit import site on startup
- `-t` - Issues warnings about inconsistent tab usage (-tt issues errors)
- `-u` - Uses unbuffered binary files for standard output and standard error (PYTHONUNBUFFERED)
- `-v` - Verbosely traces module import and cleanup actions (PYTHONVERBOSE)
- `-V` - Prints the Python version number, then terminates
- `-W arg` - Adds an entry to the warnings filter
- `-x` - Excludes (skips) the first line of the main script’s source

Use `-i` when you want to get an interactive session immediately after running some script, with top-level variables still intact and available for inspection. You do not need `-i` for normal interactive sessions, although it does no harm. `-t` and `-tt` ensure that you use tabs and spaces consistently in Python sources

#### Interactive sessions

When you run python without a script argument, Python starts an interactive ses‐ sion and prompts you to enter Python statements or expressions. Interactive ses‐ sions are useful to explore, to check things out, and to use Python as a powerful, extensible interactive calculator.

When you enter a complete statement, Python executes it. When you enter a com‐ plete expression, Python evaluates it. If the expression has a result, Python outputs a string representing the result and also assigns the result to the variable named `_` (a single underscore) so that you can immediately use that result in another expres‐ sion. The prompt string is >>> when Python expects a statement or expression and ... when a statement or expression has been started but not completed. In par‐ ticular, Python prompts you with ... when you have opened a parenthesis on a pre‐ vious line and have not closed it yet.

#### Running Python Programs

Whatever tools you use to produce your Python application, you can see your appli‐ cation as a set of Python source files, which are normal text files. A script is a file that you can run directly. A module is a file that you can import to provide functionality to other files or to interactive sessions. A Python file can be both a module (exposing functionality when imported) and a script (suit‐ able for being run directly). A useful and widespread convention is that Python files that are primarily intended to be imported as modules, when run directly, should execute some simple self-test operations.

The Python interpreter automatically compiles Python source files as needed. Python source files normally have the extension .py. In v2, Python saves the com‐ piled bytecode file for each module in the same directory as the module’s source, with the same basename and extension .pyc (or .pyo when you run Python with option -O). In v3, Python saves the compiled bytecode in subdirectory \_**\_pycache\_\_** of the directory containing the module’s source, with a version-specific extension, and annotated to denote optimization level.

Run Python with option `-B` to avoid saving compiled bytecode to disk, which can be handy when you import modules from a read-only disk. Also, Python does not save the compiled bytecode form of a script when you run the script directly; rather, Python recompiles the script each time you run it. Python saves bytecode files only for modules you import. It automatically rebuilds each module’s bytecode file when‐ ever necessary

You can run Python code interactively with the Python interpreter or an IDE. Nor‐ mally, however, you initiate execution by running a top-level script. To run a script, give its path as an argument to python. Depending on your operating system, you can invoke python directly from a shell script or command file. On Unix-like systems, you can make a Python script directly executable by setting the file’s permission bits `x` and `r` and beginning the script with a so-called `shebang` line, which is a first line such as:

`#!/usr/bin/env python`

or some other line starting with `#!` followed by a path to the python interpreter pro‐ gram, in which case you can optionally add a single word of options, for example:

`#!/usr/bin/python -O`

## Core Python Language and Built ins

#### Lexical Structure

##### Tokens

Python breaks each logical line into a sequence of elementary lexical components known as tokens. Each token corresponds to a substring of the logical line. The normal token types are identifiers, keywords, operators, delimiters, and literals, which we cover in the following sections. You may freely use whitespace between tokens to separate them. Some whitespace separation is necessary between logically adjacent identifiers or keywords; otherwise, Python would parse them as a single, longer identifier. For example, `ifx` is a single identifier; to write the keyword `if` followed by the identifier `x`, you need to insert some whitespace (e.g., `if x`).

##### Identifiers

An identifier is a name used to specify a variable, function, class, module, or other object. An identifier starts with a letter.

Normal Python style is to start class names with an uppercase letter, and other identifiers with a lowercase letter. Starting an identifier with a single leading underscore indicates by convention that the identifier is meant to be private. Starting an identi‐ fier with two leading underscores indicates a strongly private identifier; if the identi‐ fier also ends with two trailing underscores, however, this means that the identifier is a language-defined special name.

##### Keywords

Python has keywords (31 of them in v2; 33 in v3), which are identifiers that Python reserves for special syntactic uses.

1. `and` - A logical operator
2. `as` - To create an alias
3. `assert` - For debugging
4. `break` - To break out of a loop
5. `class` - To define a class
6. `continue` - To continue to the next iteration of a loop
7. `def` - To define a function
8. `del` - To delete an object
9. `elif` - Used in conditional statements, same as else if
10. `else` - Used in conditional statements
11. `except` - Used with exceptions, what to do when an exception occurs
12. `False` - Boolean value, result of comparison operations
13. `finally` - Used with exceptions, a block of code that will be executed no matter if there is an exception or not
14. `for` - To create a for loop
15. `from` - To import specific parts of a module
16. `global` - To declare a global variable
17. `if` - To make a conditional statement
18. `import` - To import a module
19. `in` - To check if a value is present in a list, tuple, etc.
20. `is` - To test if two variables are equal
21. `lambda` - To create an anonymous function
22. `None` - Represents a null value
23. `nonlocal` - To declare a non-local variable
24. `not` - A logical operator
25. `or` - A logical operator
26. `pass` - A null statement, a statement that will do nothing
27. `raise` - To raise an exception
28. `return` - To exit a function and return a value
29. `True` - Boolean value, result of comparison operations
30. `try` - To make a try...except statement
31. `while` - To create a while loop
32. `with` - Used to simplify exception handling
33. `yield` - To end a function, returns a generator

##### Operators

```
+ - * / % ** // << >> & | ^ ~ < <= > >= < > != ==
```

##### Delimiters

Python uses the following characters and combinations as delimiters in expressions, list, dictionary, and set literals, and various statements, among other purposes:

```
(  )   [  ]   {  }
,  :  .  `   =  ;  @
+=  -=  *=  /= //=  %=
&=  |=  ^=  >>=  <<=  **=
```

##### Statements

You can look at a Python source file as a sequence of simple and compound statements. Unlike some other languages, Python has no “declarations” or other top-level syntax elements: just statements.

#### Data Types

The operation of a Python program hinges on the data it handles. Data values in Python are known as objects; each object, AKA value, has a type. An object’s type determines which operations the object supports (in other words, which operations you can perform on the value). The type also determines the object’s attributes and items (if any) and whether the object can be altered. An object that can be altered is known as a mutable object, while one that cannot be altered is an immutable object.

The built-in type(obj) accepts any object as its argument and returns the type object that is the type of obj. The built-in function `isinstance(obj, type)` returns `True` when object obj has type type (or any subclass thereof ); otherwise, it returns `False`.

##### Numbers

The built-in numeric types in Python include integers (int and long, in v2; in v3, there’s no distinction between kinds of integers), floating-point numbers, and complex numbers.
`All numbers in Python are immutable objects; therefore, when you perform an operation on a number object, you produce a new number object`

##### Integer Numbers

Integer literals can be decimal, binary, octal, or hexadecimal. A `decimal literal` is a sequence of digits in which the `first digit is nonzero`. A `binary literal` is `0b followed by a sequence of binary digits (0 or 1)`. An `octal literal`, in v2 only, can be 0 followed by a sequence of `octal digits (0 to 7)`. This syntax can be quite misleading for the reader, and we do not recommend it; rather, use `0o followed by a sequence of octal digits`, which works in both v2 and v3 and does not risk misleading the reader. A `hexadecimal literal` is `0x followed by a sequence of hexadecimal digits (0 to 9 and A to F, in either upper- or lowercase)`. For example:

```python
1, 23, 3493             # Decimal integer literals
0b010101, 0b110010      # Binary integer literals
0o1, 0o27, 0o6645       # Octal integer literals
0x1, 0x17, 0xDA5        # Hexadecimal integer literals
```

##### Floating Point numbers

A floating-point literal is a sequence of decimal digits that includes a decimal point (.), an exponent suffix (an e or E, optionally followed by + or -, followed by one or more digits), or both. The leading character of a floating-point literal cannot be e or E; it may be any digit or a period (.). For example:

```python
0., 0.0, .0, 1., 1.0, 1e0, 1.e0, 1.0e0 # Floating-point literals
```

##### Complex numbers

A complex number is made up of two floating-point values, one each for the real and imaginary parts. You can access the parts of a complex object `z` as read-only attributes `z.real` and `z.imag`. You can specify an imaginary literal as a floating- point or decimal literal followed by a j or J:

```python
0j, 0.j, 0.0j, .0j, 1j, 1.j, 1.0j, 1e0j, 1.e0j, 1.0e0j
```

The `j` at the end of the literal indicates the `square root of -1`, as commonly used in electrical engineering (some other disciplines use `i` for this purpose, but Python has chosen j. There are no other complex literals. To denote any constant complex number, add or subtract a floating-point (or integer) literal and an imaginary one. `For example, to denote the complex number that equals one, use expressions like 1+0j or 1.0+0.0j. Python performs the addition or subtraction at compile time.`

##### Underscores in numeric literals

To assist visual assessment of the magnitude of a number, from 3.6 onward numeric literals can include single underscore (\_) characters between digits or after any base specifier. As this implies, not only decimal numeric constants can benefit from this new notational freedom:

```python
# grouping decimal numbers by thousands
amount = 10_000_000.0

# grouping hexadecimal addresses by words
addr = 0xCAFE_F00D

# grouping bits into nibbles in a binary literal
flags = 0b_0011_1111_0100_1110

# same, for string conversions
flags = int('0b_1111_0000', 2)
```

##### Sequences

A sequence is an ordered container of items, indexed by integers. Python has built-in sequence types known as strings (bytes and Unicode), tuples, and lists. Library and extension modules provide other sequence types, and you can write yet others yourself

##### Iterables

A Python concept that generalizes the idea of “sequence” is that of iterables. `All sequences are iterable`: whenever we say you can use an iterable, you can in particular use a sequence (for example, a list).

`Also, when we say that you can use an iterable, we mean, usually, a bounded iterable: an iterable that eventually stops yielding items. All sequences are bounded. Itera‐ bles, in general, can be unbounded, but if you try to use an unbounded iterable without special precautions, you could produce a program that never terminates, or one that exhausts all available memory.`

##### Strings

A built-in string object (bytes or Unicode) is a sequence of characters used to store and represent text-based information (byte strings, also known as byte objects, store and represent arbitrary sequences of binary bytes). Strings in Python are immutable: when you perform an operation on strings, you always produce a new string object, rather than mutating an existing string. String objects provide many methods.

`A string literal can be quoted or triple-quoted. A quoted string is a sequence of 0+ characters within matching quotes, single (') or double ("). For example:`

```python
'This is a literal string'
"This is another string"
```

`The two different kinds of quotes function identically; having both lets you include one kind of quote inside of a string specified with the other kind, with no need to escape quote characters with the backslash character (\):`

```python
'I\'m a Python fanatic' # a quote can be escaped
"I'm a Python fanatic" # this way is more readable
```

`Other things equal, using single quotes to denote string literals is better Python style. To have a string literal span multiple physical lines, you can use a \ as the last character of a line to indicate that the next line is a continuation:`

```python
'A not very long string \
that spans two lines' # comment not allowed on previous line
```

`To make the string contain two lines, you can embed a newline in the string:`

```python
'A not very long string\n\
that prints on two lines' # comment not allowed on previous line
```

`A better approach is to use a triple-quoted string, enclosed by matching triplets of quote characters (''' or, more commonly, """):`

```python
"""An even bigger
string that spans
three lines"""           # comments not allowed on previous lines
```

`In a triple-quoted string literal, line breaks in the literal remain as newline charac‐ ters in the resulting string object. You can start a triple-quoted literal with a back‐ slash immediately followed by a newline, to avoid having the first line of the literal string’s content at a different indentation level from the rest. For example:`

```python
the_text = """\
First line
Second line
""" # like 'First line\nSecond line\n' but more readable
```

The only character that cannot be part of a triple-quoted string is an unescaped backslash, while a quoted string cannot contain unescaped backslashes, nor line ends, nor the quote character that encloses it. The backslash character starts an escape sequence, which lets you introduce any character in either kind of string.

Colons can be used to align columns.

| Sequence   |                   Meaning                   |  ASCII/ISO code |
| ---------- | :-----------------------------------------: | --------------: |
| \<newline> |             Ignore end of line              |            None |
| \\\        |                  Backslach                  |            0x5c |
| \\'        |                Single Quote                 |            0x27 |
| \\"        |                Double Quote                 |            0x22 |
| \\a        |                    Bell                     |            0x07 |
| \\b        |                  Backspace                  |            0x08 |
| \\f        |                  Form Feed                  |            0x0c |
| \\n        |                   Newline                   |            0x0a |
| \\r        |               Carriage return               |            0x0d |
| \\t        |                     Tab                     |            0x09 |
| \\v        |                Vertical Tab                 |            0x0b |
| \\DDD      |               Octal value DDD               |        As Given |
| \\xXX      |             Hexadecimal valueXX             |        As Given |
| \\other    | Any other character: a two-character string | 0x5c + as given |

###### Raw String Literal

A variant of a string literal is a raw string. The syntax is the same as for quoted or triple-quoted string literals, except that an r or R immediately precedes the leading quote. In raw strings, escape sequences are not interpreted as in Table 3-1, but are literally copied into the string, including backslashes and newline characters. Raw string syntax is handy for strings that include many backslashes, especially regular expression patterns. A raw string cannot end with an odd number of backslashes: the last one would be taken as escaping the terminating quote.

###### Unicode String Literal

In Unicode string literals you can use \u followed by four hex digits, and \U followed by eight hex digits, to denote Unicode characters, and can also include the same escape sequences listed in above table. Unicode literals can also include the escape sequence `\N{name}`, where name is a standard Unicode name, as listed at http://www.unicode.org/charts/. For example, `\N{Copyright Sign}` indicates a Uni‐ code copyright sign character (©).

###### Formatted String Literal (New in 3.6)

Formatted string literals let you inject formatted expressions into your strings, which are therefore no longer constants but subject to evaluation at execution time.

```python
>>> name = "Ameer"
>>> age = 24
>>> f"Hello, {name}. You are {age}."
'Hello, Ameer. You are 24.'
```

You could also call functions.

```python
>>> def to_lowercase(input):
...     return input.lower()

>>> name = "ameer"
>>> f"{to_lowercase(name)} is funny."
'ameer is funny.'
```

Multiple string literals of any kind—quoted, triple-quoted, raw, bytes, formatted, Unicode can be adjacent, with optional whitespace in between (except that, in v3, you cannot mix bytes and Unicode in this way). The compiler concatenates such adjacent string literals into a single string object. In v2, if any literal in the concatenation is Unicode, the whole result is Unicode. Writing a long string literal in this way lets you present it readably across multiple physical lines and gives you an opportunity to insert comments about parts of the string. For example:

```python
marypop = ('supercalifragilistic' # Open paren->logical line continues
            'expialidocious') # Indentation ignored in continuation
```

The string assigned to marypop is a single word of 34 characters.

##### Tuples

A tuple is an immutable ordered sequence of items. The items of a tuple are arbi‐ trary objects and may be of different types. You can use mutable objects (e.g., lists) as tuple items; however, best practice is to avoid tuples with mutable items.
To denote a tuple, use a series of expressions (the items of the tuple) separated by commas (,); if every item is a literal, the whole assembly is a tuple literal. You may optionally place a redundant comma after the last item. You may group tuple items within parentheses, but the parentheses are necessary only where the commas would otherwise have another meaning (e.g., in function calls), or to denote empty or nested tuples. A tuple with exactly two items is also known as a pair. To create a tuple of one item, add a comma to the end of the expression. To denote an empty tuple, use an empty pair of parentheses. Here are some tuple literals, all in the optional parentheses (the parentheses are not optional in the last case):

```python
(100, 200, 300)     # Tuple with three items
(3.14,)             # Tuple with 1 item needs trailing comma
()                  # Empty tuple (parentheses NOT optional)
```

You can also call the built-in type `tuple` to create a tuple. For example:
`tuple('wow')`
This builds a tuple equal to that denoted by the tuple literal:
`('w', 'o', 'w')`
tuple() without arguments creates and returns an empty tuple, like (). When x is
iterable, tuple(x) returns a tuple whose items are the same as those in x.

##### Lists

A list is a mutable ordered sequence of items. The items of a list are arbitrary objects and may be of different types.

```python
[42, 3.14, 'hello']         # List with three items
[100]                       # List with one item
[]                          # Empty list
```

You can also call the built-in type lis`t to create a list. For example`list('wow')`This builds a list equal to that denoted by the list literal:`['w', 'o', 'w']`

##### Sets

Python has two built-in set types, `set` and `frozenset`, to represent arbitrarily ordered collections of unique items. Items in a set may be of different types, but they must be hashable. `Instances of type set are mutable, and thus, not hashable;` `instances of type frozenset are immutable and hashable`. You can’t have a set whose items are sets, but you can have a set (or frozenset) whose items are frozensets. Sets and frozensets are not ordered.

To create a set, you can call the `built-in type set` with no argument (this means an empty set) or one argument that is iterable (this means a set whose items are those of the iterable). You can similarly build a frozenset by calling frozenset.

```python
{42, 3.14, 'hello'}           # Literal for a set with three items
{100}                         # Literal for a set with one item
set()                         # Empty set (can't use {}—empty dict!)
```

##### Dictionaries

A mapping is an arbitrary collection of objects indexed by nearly arbitrary values called keys. Mappings are mutable and, like sets but unlike sequences, are not (necessarily) ordered.

Python provides a single built-in mapping type: the dictionary type. Library and extension modules provide other mapping types, and you can write others yourself.
`Keys in a dictionary may be of different types, but they must be hashable`. `Values in a dictionary are arbitrary objects and may be of any type`. An item in a dictionary is a key/value pair.

To denote a dictionary, you can use a series of colon-separated pairs of expressions (the pairs are the items of the dictionary) separated by commas (,) within braces ({});
`dictionaries do not allow duplicate keys.`

```python
{'x':42, 'y':3.14, 'z':7}      # Dictionary with three items, str keys
{1:2, 3:4}                     # Dictionary with two items, int keys
{1:'za', 'br':23}              # Dictionary with mixed key types
{}                             # Empty dictionary
```

You can also call the built-in type dict to create a dictionary in a way that, while usually less concise, can sometimes be more readable.

```python
dict(x=42, y=3.14, z=7)            # Dictionary with three items, str keys
dict([(1, 2), (3, 4)])             # Dictionary with two items, int keys
dict([(1,'za'), ('br',23)])        # Dictionary with mixed key types
dict()                             # Empty dictionary
```

You can also create a dictionary by callingdict.fromkeys. The first argument is an iterable whose items become the keys of the dictionary; the second argument is the value that corresponds to each and every key (all keys initially map to the same value). If you omit the second argument, it defaults to None. For example:

```python
dict.fromkeys('hello', 2)       # same as {'h':2, 'e':2, 'l':2, 'o':2}
dict.fromkeys([1, 2, 3])        # same as {1:None, 2:None, 3:None}
```

##### None

The built-in None denotes a null object. None has no methods or other attributes. You can use None as a placeholder when you need a reference but you don’t care what object you refer to, or when you need to indicate that no object is there. Functions return None as their result unless they have specific return statements coded to return other values.

##### Callables

In Python, callable types are those whose instances support the function call operation.
Functions are callable. Python provides several built-in functions and supports userdefined functions. Generators are also callable.
`Types are also callable, as we already saw for the dict, list, set, and tuple built-in types.`
Class objects (user-defined types) are also callable. Calling a type normally creates and returns a new instance of that type.
Other callables are methods, which are functions bound to class attributes, and instances of classes that supply a special method named \_\_call\_\_.

##### Boolean Values

`Any data value in Python can be used as a truth value: true or false`. Any nonzero number or nonempty container (e.g., string, tuple, list, set, or dictionary) is true. 0 (of any numeric type), None, and empty containers are false.
The built-in type bool is a subclass of int. **The only two values of type bool are True and False, which have string representations of 'True' and 'False', but also numerical values of 1 and 0**, respectively. Several built-in functions return bool results, as do comparison operators.
You can call bool(x) with any x as the argument. The result is True when x is true and False when x is false. Good Python style is not to use such calls when they are redundant, as they most often are:
**always write`if x`:, never any of `if bool(x)`:, `if x is True`, `if x==True`:, `if bool(x)==True`.**
However, you can use bool(x) to count the number of true items in a sequence. For example:

```python
def count_trues(seq): return sum(bool(x) for x in seq)
```

In this example, the bool call ensures each item of seq is counted as 0 (if false) or 1
(if true), so count_trues is more general than sum(seq) would be.
`When we write “expression is true,” we mean that bool(expression) would return True.`

#### Variables and Other References

A Python program accesses data values through references. A reference is a “name” that refers to a value (object). References take the form of variables, attributes, and items. In Python, a variable or other reference has no intrinsic type. The object to which a reference is bound at a given time always has a type, but a given reference may be bound to objects of various types in the course of the program’s execution.

##### Variables

In Python, there are no “declarations.” The existence of a variable begins with a statement that binds the variable (in other words, sets a name to hold a reference to some object). You can also unbind a variable, resetting the name so it no longer holds a reference. Assignment statements are the most common way to bind vari‐ ables and other references. The del statement unbinds references.`The cleanup of objects with no references is known as garbage collection.` A variable can be global or local. A global variable is an attribute of a module object. A local variable lives in a function’s local namespace

###### Object attributes and items

To denote an attribute of an object, use a reference to the object, followed by a period (.), followed by an identifier known as the attribute name. For example, x.y refers to one of the attributes of the object bound to name x, specifically that attribute whose name is 'y'.

To denote an item of an object, use a reference to the object, followed by an expres‐ sion within brackets ([]). The expression in brackets is known as the item’s index or key, and the object is known as the item’s container. For example, x[y] refers to the item at the key or index bound to name y, within the container object bound to name x.

Attributes that are callable are also known as methods. Python draws no strong dis‐ tinctions between callable and noncallable attributes, as some other languages do. All rules about attributes also apply to callable attributes (methods).

###### Accessing nonexistent references

A common programming error is trying to access a reference that does not exist. For example, a variable may be unbound, or an attribute name or item index may not be valid for the object to which you apply it. The Python compiler, when it ana‐ lyzes and compiles source code, diagnoses only syntax errors. Compilation does not diagnose semantic errors, such as trying to access an unbound attribute, item, or variable. Python diagnoses semantic errors only when the errant code executes— that is, at runtime. When an operation is a Python semantic error, attempting it raises an exception. Accessing a nonexistent variable, attribute, or item—just like any other semantic error—raises an exception.

##### Assignment Statements

Assignment statements can be plain or augmented.

###### Plain assignment

A plain assignment statement in the simplest form has the syntax:

    `target = expression`

`The target is known as the lefthand side (LHS)`, and `the expression is the righthand side (RHS)`. When the assignment executes, Python evaluates the RHS expression, then binds the expression’s value to the LHS target. Python draws no strong distinction between call‐ able and noncallable objects. **This is part of functions and the like being first-class objects.**

Details of the binding do depend on the kind of target. The target in an assignment may be an identifier, an attribute reference, an indexing, or a slicing:

- `An identifier`
  Is a variable name. Assigning to an identifier binds the variable with this name.
- `An attribute reference`
  Has the syntax `obj.name`. Assigning to an attribute reference asks object obj to bind its attribute named `name`.
- `An indexing`
  Has the syntax `obj[expr]`. Assigning to an indexing asks container obj to bind its item indicated by the value of expr, also known as the index or key of the item in the container.
- `A slicing`
  Has the syntax `obj[start:stop]` or `obj[start:stop:stride]`. Assigning to a slicing asks con‐ tainer obj to bind or unbind some of its items. Assigning to a slicing such as `obj[start:stop:stride]` is equivalent to assigning to the indexing `obj[slice(start, stop, stride)]`.

A plain assignment can use multiple targets and equals signs (=). For example:

      `a = b = c = 0`

The target in a plain assignment can list two or more references separated by commas, optionally enclosed in parentheses or brackets. For example:

      `a , b , c = x`

**This statement requires x to be an iterable with exactly three items, and binds a to the first item, b to the second, and c to the third. This kind of assignment is known as an unpacking assignment.**

An unpacking assignment can also be used to swap references:

      `a , b = b , a`

`In v3, exactly one of the multiple targets of an unpacking assignment may be preceded by *. That starred target is bound to a list of all items, if any, that were not assigned to other targets.`

```python
first, *middle, last = x      # x is a list,
```

Assignment requires x to have at least two items.

###### Augmented assignment

An augmented assignment (sometimes also known as an in-place assignment) differs from a plain assignment in that, instead of an equals sign (=) between the target and the expression, it uses an augmented operator, which is a binary operator followed by =. The augmented operators are

```python
+=, -=, \*=, /=, //=, %=, \*\*=, |=, >>=, <<=, &=, and ^= (and, in v3 only, @=).
```

An augmented assignment can have only one target on the LHS; augmented assignment doesn’t support multiple targets.

In an augmented assignment, just as in a plain one, Python first evaluates the RHS expression. Then, when the LHS refers to an object that has a special method for the appropriate in-place version of the operator, Python calls the method with the RHS value as its argument. It is up to the method to modify the LHS object appropriately and return the modified object (“Special Methods” on page 123 covers special meth‐ ods). When the LHS object has no appropriate in-place special method, Python applies the corresponding binary operator to the LHS and RHS objects, then rebinds the target reference to the operator’s result. For example, x+=y is like x=x.**\_\_iadd\_\_**(y) when x has special method **\_\_iadd\_\_** for in-place addition. Otherwise, x+=y is like x=x+y.

Augmented assignment never creates its target reference; the target must already be bound when augmented assignment executes. Augmented assignment can rebind the target reference to a new object, or modify the same object to which the target reference was already bound. Plain assignment, in contrast, can create or rebind the LHS target reference, but it never modifies the object, if any, to which the target ref‐ erence was previously bound. The distinction between objects and references to objects is crucial here. For example,

`x=x+y does not modify the object to which name x was originally bound. Rather, it rebinds the name x to refer to a new object. x+=y, in contrast, modifies the object to which the name x is bound, when that object has special method __iadd__; otherwise, x+=y rebinds the name x to a new object, just like x=x+y.`

###### Del Statements

Despite its name, a del statement unbinds references—it does not, per se, delete objects. Object deletion may automatically follow as a consequence, by garbage col‐ lection, when no more references to an object exist.

A del statement consists of the keyword del, followed by one or more target refer‐ ences separated by commas (,). Each target can be a variable, attribute reference, indexing, or slicing, just like for assignment statements, and must be bound at the time del executes. When a del target is an identifier, the del statement means to unbind the variable. If the identifier was bound, unbinding it is never disallowed; when requested, it takes place.

Containers are also allowed to have del cause side effects. For example, assuming del C[2] succeeds, when C is a dict, this makes future references to C[2] invalid (raising KeyError) until and unless you assign to C[2] again; but when C is a list, del C[2] implies that every following item of C “shifts left by one”—so, if C is long enough, future references to C[2] are still valid, but denote a distinct item than they did before the del.
