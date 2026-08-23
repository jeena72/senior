# Python Questions for Senior and Lead roles

<img src="https://user-images.githubusercontent.com/67960818/159924991-ad7ac6de-facf-4cb0-a8c9-31a7407fb9e4.png" alt="python-logo-master-v3-TM-flattened" style="max-width: 100%;">

This repository contains questions and answers for Senior and Lead Python developers. The material is divided into several parts:

> **Python version status (August 2026):** the current stable release is **Python 3.14** (latest patch: 3.14.7). **Python 3.15** is in the release-candidate phase and is scheduled for final release in October 2026. Python 3.9 reached end-of-life in October 2025, and Python 3.10 reaches end-of-life in October 2026 — actively supported versions are 3.10–3.14.

## Main Sections
- [Python Technical Questions](#python-technical-questions)
- [Engineering Practices: tooling, packaging, web stack, Docker, security](engineering_practices.md)
- [AI-Assisted Development with Claude Code](claude_code.md)
- [PostgreSQL Questions](postgresql.md)
- [Common Questions for Senior and Lead Developers](common_questions.md)
- [Release Strategy](release_strategy.md)
- [Code Standards](code_standards.md)
- [Cross-discipline Questions](cross_discipline.md)

## Python Technical Questions
- [Mutable and Immutable Objects](#mutable-and-immutable-objects)
  * [Mutable objects](#mutable-objects)
  * [Immutable objects](#immutable-objects)
  * [Features](#features)
  * [How objects are passed to Functions](#how-objects-are-passed-to-functions)
- [Ways to execute Python code: exec, eval, ast, code, codeop, etc.](#ways-to-execute-python-code-exec-eval-ast-code-codeop-etc)
- [Advanced differences between 2.x and 3.x in general](#advanced-differences--between-2x-and-3x-in-general)
  + [Division operator](#division-operator)
  + [`print` function](#print-function)
  + [Unicode](#unicode)
  + [`xrange`](#xrange)
  + [Error Handling](#error-handling)
  + [`_future_` module](#_future_-module)
  + [Six](#six)
- [`deepcopy`, method `copy`, slicing, etc.](#deepcopy-method-copy-slicing-etc)
- [OrderedDict, DefaultDict](#ordereddict-defaultdict)
- [Hashable Objects](#hashable-objects)
- [Strong and weak typing](#strong-and-weak-typing)
- [Frozenset](#frozenset)
- [Weak references](#weak-references)
- [Raw strings](#raw-strings)
- [Unicode and ASCII strings](#unicode-and-ascii-strings)
- [Python Statements and Syntax](#python-statements-and-syntax)
  * [Iteration protocol.](#iteration-protocol)
  * [Generators](#generators)
  * [yield](#yield)
  * [method send(), throw(), next(), close()](#method-send-throw-next-close)
  * [Coroutines](#coroutines)
  * [asyncio Deep Dive: Tasks, TaskGroup, Cancellation](#asyncio-deep-dive-tasks-taskgroup-cancellation)
  * [Context Variables (contextvars)](#context-variables-contextvars)
  * [Pattern Matching (Python 3.10+)](#pattern-matching-python-310)
  * [Advanced Pattern Matching](#advanced-pattern-matching)
  * [Exception Groups (Python 3.11+)](#exception-groups-python-311)
  * [Exception Design and Chaining](#exception-design-and-chaining)
  * [Type Parameter Syntax (Python 3.12+)](#type-parameter-syntax-python-312)
  * [Typing Deep Dive: Protocol, TypedDict, Generics, ParamSpec](#typing-deep-dive-protocol-typeddict-generics-paramspec)
  * [Per-Interpreter GIL (Python 3.12+)](#per-interpreter-gil-python-312)
  * [Free-Threaded Python (Python 3.13+, Official since 3.14)](#free-threaded-python-python-313-official-since-314)
  * [JIT Compiler (Python 3.13+, Experimental)](#jit-compiler-python-313-experimental)
  * [Improved Interactive Interpreter (Python 3.13+)](#improved-interactive-interpreter-python-313)
  * [Platform Support (Python 3.13+)](#platform-support-python-313)
  * [Template Strings (Python 3.14+)](#template-strings-python-314)
  * [Deferred Evaluation of Annotations (Python 3.14+)](#deferred-evaluation-of-annotations-python-314)
  * [Other Python 3.14 Improvements](#other-python-314-improvements)
  * [What's Coming in Python 3.15](#whats-coming-in-python-315)
- [Functions in Python](#functions-in-python)
  * [When and how many times are default arguments evaluated?](#when-and-how-many-times-are-default-arguments-evaluated)
  * [`partial`](#partial)
  * [`functools` Deep Dive: Caching, Dispatch, Ordering](#functools-deep-dive-caching-dispatch-ordering)
  * [Best practice decorators for functions](#best-practice-decorators-for-functions)
  * [Decorator](#decorator)
  * [Decorator factory (passing args to decorators)](#decorator-factory-passing-args-to-decorators)
  * [`wraps`](#wraps)
  * [Decorator for class](#decorator-for-class)
  * [Indirect function calls](#indirect-function-calls)
  * [Function introspection](#function-introspection)
  * [Implementation details of functional programming, for vs map](#implementation-details-of-functional-programming-for-vs-map)
- [Scopes in Python](#scopes-in-python)
  * [LEGB rule](#legb-rule)
  * [`global` and `nonlocal`](#global-and-nonlocal)
    + [The `global` Statement](#the-global-statement)
    + [The `nonlocal` Statement](#the-nonlocal-statement)
  * [Scopes and nested functions, closures](#scopes-and-nested-functions-closures)
  * [globals() и locals(): Meaning, could we change both of them?](#globals-%D0%B8-locals-meaning-could-we-change-both-of-them)
- [Modules in Python](#modules-in-python)
  * [Module `reload`, `importlib`](#module-reload-importlib)
- [OOP in Python](#oop-in-python)
  * [SOLID](#solid)
  * [The four basics of object-oriented programming](#the-four-basics-of-object-oriented-programming)
  * [abstract base class](#abstract-base-class)
  * [getattr(), setattr()](#getattr-setattr)
  * [`__getattr__`, `__setattr__`, `__delattr__`](#__getattr__-__setattr__-__delattr__)
  * [`__getattribute__`](#__getattribute__)
  * [Name mangling](#name-mangling)
  * [@property(getter, setter, deleter)](#propertygetter-setter-deleter)
  * [Descriptor Protocol](#descriptor-protocol)
  * [init, repr, str, cmp, new , del, hash, nonzero, unicode, class operators](#init--repr-str-cmp--new--del--hash-nonzero-unicode-class-operators)
  * [Rich comparison methods](#rich-comparison-methods)
  * [`__call__`](#__call__)
  * [Multiple inheritance](#multiple-inheritance)
  * [Classic algorithm](#classic-algorithm)
  * [Diamond problem](#diamond-problem)
  * [MRO, super](#mro-super)
  * [Mixins](#mixins)
  * [metaclass definition](#metaclass-definition)
  * [`__init_subclass__`, `__set_name__`, `__class_getitem__`](#__init_subclass__-__set_name__-__class_getitem__)
  * [type(), isinstance(), issubclass()](#type-isinstance-issubclass)
    + [`type()` Return Value](#type-return-value)
  * [`__slots__`](#__slots__)
  * [dataclasses vs NamedTuple vs TypedDict](#dataclasses-vs-namedtuple-vs-typeddict)
- [Troubleshooting in Python](#troubleshooting-in-python)
  * [Types of profilers: Static and dynamic profilers](#types-of-profilers-static-and-dynamic-profilers)
    + [`trace` module](#trace-module)
    + [`faulthandler` module](#faulthandler-module)
    + [application performance monitoring (APM) tools that fit](#application-performance-monitoring-apm-tools-that-fit)
    + [What part of the code should I profile?](#what-part-of-the-code-should-i-profile)
    + [Typically, we profile:](#typically-we-profile)
    + [What metrics should I profile?](#what-metrics-should-i-profile)
    + [Memory profiling](#memory-profiling)
    + [Deterministic profiling versus statistical profiling](#deterministic-profiling-versus-statistical-profiling)
    + [`pyinstrument`](#pyinstrument)
    + [`py-spy` and `scalene`](#py-spy-and-scalene)
  * [`resource` module](#resource-module)
  * [context managers contextlib decorator, with-enabled class](#context-managers-contextlib-decorator-with-enabled-class)
  * [`contextlib` Beyond `@contextmanager`](#contextlib-beyond-contextmanager)
- [Unit testing in Python](#unit-testing-in-python)
  * [Mock objects](#mock-objects)
  * [Coverage](#coverage)
  * [Testing Frameworks: pytest, unittest, doctests](#testing-frameworks-pytest-unittest-doctests)
  * [pytest in depth: fixtures, parametrize, monkeypatch](#pytest-in-depth-fixtures-parametrize-monkeypatch)
- [Memory management in Python](#memory-management-in-python)
  * [3 generations of GC](#3-generations-of-gc)
    + [module gc](#module-gc)
    + [Which type of objects are tracked?](#which-type-of-objects-are-tracked)
  * [recommendations for GC usage](#recommendations-for-gc-usage)
  * [Memory leaks/deleters issues](#memory-leaksdeleters-issues)
- [Threading and multiprocessing in Python](#threading-and-multiprocessing-in-python)
  * [GIL (Definition, algorithms in 2.x and 3.x)](#gil-definition-algorithms-in-2x-and-3x)
  * [Threads(modules thread, threading; class Queue; locks)](#threadsmodules-thread-threading-class-queue-locks)
  * [Processes(multiprocessing, Process, Queue, Pipe, Value, Array, Pool, Manager)](#processesmultiprocessing-process-queue-pipe-value-array-pool-manager)
  * [Choosing a concurrency model: a decision guide](#choosing-a-concurrency-model-a-decision-guide)
  * [How to avoid GIL restrictions (C extensions)](#how-to-avoid-gil-restrictions-c-extensions)
- [Distributing and documentation in Python](#distributing-and-documentation-in-python)
  * [Modern packaging: pyproject.toml, PEP 517/518/621](#modern-packaging-pyprojecttoml-pep-517518621)
  * [Documentation autogeneration: sphinx, pydoc, etc.](#documentation-autogeneration-sphinx-pydoc-etc)
- [Python and C interaction](#python-and-c-interaction)
  * [C ext API,call C from python, call python from C](#c-ext-apicall-c-from-python-call-python-from-c)
  * [cffi, swig, SIP, boost-python](#cffi-swig-sip-boost-python)
    + [Boost](#boost)
- [Python tools](#python-tools)
  * [Python standard library](#python-standard-library)
  * [Advanced knowledge of standard library:](#advanced-knowledge-of-standard-library)

## Mutable and Immutable Objects

### Mutable objects:

list, dict, set, bytearray

### Immutable objects:
- int, float, complex, string, 
- tuple (the "value" of an immutable object can't change, but its constituent objects can.), 
- frozenset [note: immutable version of set], 
- bytes

### Features:

- Mutable objects are great to use when you need to change the size of the object, example list, dict etc.. Immutables are used when you need to ensure that the object you made will always stay the same.
- Immutable objects are fundamentally expensive to "change", because doing so involves creating a new object. Changing mutable objects is cheap.
- Immutability makes objects safe to use as `dict` keys / `set` members (hashable) and safe to share between threads without locks.

### How objects are passed to Functions

**Python is neither call-by-value nor call-by-reference — it is "call by object reference" (also called "call by assignment"), uniformly for ALL types.** Nothing is ever copied when you pass an argument: the parameter name is simply bound to the same object the caller passed.

The *observable* difference between mutable and immutable arguments comes from what you can do with that shared object, not from how it was passed:

```python
def modify(lst, num):
    lst.append(4)     # mutates the SHARED list - caller sees it
    num += 1          # rebinds the LOCAL name to a new int - caller does not see it

items, count = [1, 2, 3], 10
modify(items, count)
print(items, count)   # [1, 2, 3, 4] 10
```

- Mutating a mutable argument in place (`lst.append`) is visible to the caller, because both names refer to one object.
- *Rebinding* the parameter (`num += 1`, `lst = []`) never affects the caller — it just points the local name elsewhere.

**Why the "call by value / call by reference" framing is wrong (and a classic interview trap):** in true call-by-value the callee would get a copy (it doesn't — `id()` is identical inside and outside); in true call-by-reference the callee could rebind the caller's *variable* (it can't). If you need the caller's object protected from mutation, pass a copy explicitly (`modify(items.copy())`) or use an immutable type.

## Ways to execute Python code: exec, eval, ast, code, codeop, etc.

The `exec(object, globals, locals)` method executes the dynamically created program, which is either a string or a code object. Returns `None`. Only side effect matters!

Example 1:
```python
program = 'a = 5\nb=10\nprint("Sum =", a+b)'
exec(program)
```
```bash
Sum = 15
```

Example 2:
```python
globals_parameter = {'__builtins__' : None}
locals_parameter = {'print': print, 'dir': dir}
exec('print(dir())', globals_parameter, locals_parameter)
```
```bash
['dir', 'print']
```

The `eval(expression, globals=None, locals=None)` method parses the expression passed to this method and runs python expression (code) within the program. Returns the value of expression!

```python
>>> a = 5
>>> eval('37 + a')   # it is an expression
42
>>> exec('37 + a')   # it is an expression statement; value is ignored (None is returned)
>>> exec('a = 47')   # modify a global variable as a side effect
>>> a
47
>>> eval('a = 47')  # you cannot evaluate a statement
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<string>", line 1
    a = 47
      ^
SyntaxError: invalid syntax
```

If a `code` object (which contains Python bytecode) is passed to `exec` or `eval`, they behave identically, excepting for the fact that exec ignores the return value, still returning `None` always. So it is possible use `eval` to execute something that has statements, if you just compiled it into bytecode before instead of passing it as a string:
```python
>>> eval(compile('if 1: print("Hello")', '<string>', 'exec'))
Hello
>>>
```

`Abstract Syntax Trees`, ASTs, are a powerful feature of Python. You can write programs that inspect and modify Python code, after the syntax has been parsed, but before it gets compiled to byte code. That opens up a world of possibilities for introspection, testing, and mischief.

In addition to compiling source code to bytecode, `compile` supports compiling abstract syntax trees (parse trees of Python code) into `code` objects; and source code into abstract syntax trees (the `ast.parse` is written in Python and just calls `compile(source, filename, mode, PyCF_ONLY_AST))`; these are used for example for modifying source code on the fly, and also for dynamic code creation, as it is often easier to handle the code as a tree of nodes instead of lines of text in complex cases.

The `code` module provides facilities to implement read-eval-print loops in Python. Two classes and convenience functions are included which can be used to build applications which provide an **interactive interpreter prompt**.

The `codeop` module provides utilities upon which the Python read-eval-print loop can be emulated, as is done in the `code` module. As a result, you probably don't want to use the module directly; if you want to include such a loop in your program you probably want to use the code module instead.

## Advanced differences  between 2.x and 3.x in general

### Division operator
If we are porting our code or executing python 3.x code in python 2.x, it can be dangerous if integer division changes go unnoticed (since it doesn't raise any error). It is preferred to use the floating value (like 7.0/5 or 7/5.0) to get the expected result when porting our code. 
### `print` function
This is the most well-known change. In this, the print keyword in Python 2.x is replaced by the print() function in Python 3.x. However, parentheses work in Python 2 if space is added after the print keyword because the interpreter evaluates it as an expression. 
### Unicode
In Python 2, an implicit str type is ASCII. But in Python 3.x implicit str type is Unicode. 

### `xrange`
xrange() of Python 2.x doesn't exist in Python 3.x. In Python 2.x, range returns a list i.e. range(3) returns [0, 1, 2] while xrange returns a xrange object i. e., xrange(3) returns iterator object which works similar to Java iterator and generates number when needed. 

### Error Handling
There is a small change in error handling in both versions. In python 3.x, 'as' keyword is required. 

### `_future_` module
The idea of the __future__ module is to help migrate to Python 3.x. 
If we are planning to have Python 3.x support in our 2.x code, we can use _future_ imports in our code. 

### Six
Six is a Python 2 and 3 compatibility library. It provides utility functions for smoothing over the differences between the Python versions with the goal of writing Python code that is compatible on both Python versions. See the documentation for more information on what is provided.

## `deepcopy`, method `copy`, slicing, etc.
The `copy()` returns a shallow copy of list and `deepcopy()` return a deep copy of list.
Python `slice()` function returns a slice object. 

A sequence of objects of any type(`string`, `bytes`, `tuple`, `list` or `range`) or the object which implements `__getitem__()` and `__len__()` method then this object can be sliced using `slice()` method.

## OrderedDict, DefaultDict
An OrderedDict is a dictionary subclass that remembers the order that keys were first inserted.

**Important note for Python 3.7+:** Since Python 3.7, regular `dict` objects are guaranteed to maintain insertion order as part of the language specification. However, `OrderedDict` still provides additional features:

| Feature | `dict` | `OrderedDict` |
|---------|--------|---------------|
| Equality comparison | Order-independent | Order-sensitive (two OrderedDicts with same items but different order are not equal) |
| `move_to_end(key, last=True/False)` | Not available | Moves key to either end efficiently |
| `popitem(last=True/False)` | Only pops from the end (LIFO) | Can pop from either end (LIFO or FIFO) |
| Memory usage | Lower | Higher |
| Reordering performance | Not optimized | Optimized for frequent reordering |

Use `OrderedDict` when you need order-sensitive equality checks, `move_to_end()`, or bidirectional `popitem()`.

`Defaultdict` is a container like dictionaries present in the module collections. `Defaultdict` is a sub-class of the dictionary class that returns a dictionary-like object. The functionality of both dictionaries and defaultdict are almost same except for the fact that defaultdict never raises a KeyError. It provides a default value for the key that does not exists.

```python
from collections import defaultdict

def def_value():
    return "Not Present"

d = defaultdict(def_value)
```

## Hashable Objects

An object is hashable if it has a hash value that does not change during its entire lifetime. Python has a built-in `hash()` function and objects implement hashing via the `__hash__()` method. For comparing, it needs `__eq__()` method (note: `__cmp__()` was removed in Python 3). If hashable objects are equal, they must have the same hash value.

**Note:** There is no built-in `hashable()` function in Python. To check if an object is hashable, you can use:
```python
from collections.abc import Hashable
isinstance(obj, Hashable)  # Returns True if hashable
# or simply try:
try:
    hash(obj)
    print("Hashable")
except TypeError:
    print("Not hashable")
```

All immutable built-in objects in Python are hashable (int, str, tuple, frozenset) while mutable containers (list, dict, set) are not hashable.

`lambda` and user-defined functions are hashable (they hash by identity).

Objects hashed using `hash()` produce irreversible values (one-way function).
`hash()` raises `TypeError` for unhashable objects, which can be used to check mutability.

## Strong and weak typing

Python is strongly, dynamically typed.

* **Strong** typing means that the type of value doesn't change in unexpected ways. A string containing only digits doesn't magically become a number, as may happen in Perl. Every change of type requires an explicit conversion.
* **Dynamic** typing means that runtime objects (values) have a type, as opposed to static typing where variables have a type.

```python
bob = 1
bob = "bob"
```

This works because the variable does not have a type; it can name any object. After `bob = 1`, you'll find that `type(bob)` returns `int`, but after `bob = "bob"`, it returns `str`.

## Frozenset
The `frozenset()` function returns an immutable frozenset object initialized with elements from the given iterable.

Frozen set is just an immutable version of a Python `set` object. While elements of a set can be modified at any time, elements of the frozen set remain the same after creation.

Due to this, frozen sets can be used as keys in Dictionary or as elements of another set. But like sets, it is not ordered (the elements can be set at any index).

## Weak references
Python contains the ``weakref`` module that creates a weak reference to an object. If there are no strong references to an object, the garbage collector is free to use the memory for other purposes.

Weak references are used to implement caches and mappings that contain massive data.

## Raw strings

Python raw string is created by prefixing a string literal with 'r' or 'R'. Python raw string treats backslash (\) as a literal character. This is useful when we want to have a string that contains backslash and don't want it to be treated as an escape character.


## Unicode and ASCII strings	

Unicode is international standard where a mapping of individual characters and a unique number is maintained. Python's `unicodedata` module uses the Unicode Character Database (UCD). Python 3.13 uses Unicode 15.1.0, and as of Python 3.14+, Python uses **Unicode 16.0.0** (released September 2024), which contains over 154,000 characters including different scripts (English, Hindi, Chinese, Japanese, etc.) as well as emojis. These characters are each represented by a unicode code point. So unicode code points refer to actual characters that are displayed.
These code points are encoded to bytes and decoded from bytes back to code points. Examples: Unicode code point for alphabet a is U+0061, emoji 🖐 is U+1F590, and for Ω is U+03A9.

The main takeaways in Python are:
1. Python 2 uses str type to store bytes and unicode type to store unicode code points. All strings by default are `str` type — which is bytes~ And Default encoding is ASCII. So if an incoming file is Cyrillic characters, Python 2 might fail because ASCII will not be able to handle those Cyrillic Characters. In this case, we need to remember to use decode("utf-8") during reading of files. This is inconvenient.
2. Python 3 came and fixed this. Strings are still `str` type by default but they now mean unicode code points instead — we carry what we see. If we want to store these `str` type strings in files we use bytes type instead. Default encoding is UTF-8 instead of ASCII. Perfect!

# Python Statements and Syntax

## Iteration protocol.

Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods `__iter__()` and `__next__()`.

## Generators
Generators are iterators, a kind of iterable you can only iterate over once. Generators do not store all the values in memory, they generate the values on the fly

## yield
`yield` is a keyword that is used like `return`, except the function will return a generator.
To master `yield`, you must understand that when you call the function, the code you have written in the function body does not run. The function only returns the generator object, this is a bit tricky.

## method send(), throw(), next(), close()

`send()` - sends value to generator, send(None) must be invoked at generator init.

```python
def double_number(number):
    while True:
        number *= 2
        number = yield number
```

`throw()` - throw custom exception. Useful for databases:

```python
def add_to_database(connection_string):
    db = mydatabaselibrary.connect(connection_string)
    cursor = db.cursor()
    try:
        while True:
            try:
                row = yield
                cursor.execute('INSERT INTO mytable VALUES(?, ?, ?)', row)
            except CommitException:
                cursor.execute('COMMIT')
            except AbortException:
                cursor.execute('ABORT')
    finally:
        cursor.execute('ABORT')
        db.close()
```

## Coroutines
Coroutines declared with the `async`/`await` syntax is the preferred way of writing asyncio applications. For example, the following snippet of code (requires Python 3.7+) prints "hello", waits 1 second, and then prints "world":
```python
>>> import asyncio

>>> async def main():
...     print('hello')
...     await asyncio.sleep(1)
...     print('world')

>>> asyncio.run(main())
hello
world
```

## asyncio Deep Dive: Tasks, TaskGroup, Cancellation

A coroutine object does nothing until it is awaited or wrapped in a **Task**. A `Task` is a coroutine scheduled on the event loop that runs concurrently with whatever awaits it. Everything senior-level in asyncio comes down to: who owns the task, and what happens when it fails or is cancelled.

### Key Features:
- `asyncio.TaskGroup` (3.11+) — structured concurrency: the block does not exit until every child finishes; a failure cancels the siblings.
- `asyncio.timeout()` / `timeout_at()` (3.11+) — context-manager timeouts that apply to a whole block.
- `CancelledError` inherits from **`BaseException`**, not `Exception` — `except Exception` must not swallow it.
- `asyncio.to_thread()` — the only correct way to call blocking code from a coroutine.

### TaskGroup instead of gather

```python
import asyncio

async def fetch(name: str, delay: float) -> str:
    await asyncio.sleep(delay)
    if name == "b":
        raise RuntimeError("b failed")
    return f"{name} ok"

async def main() -> None:
    try:
        async with asyncio.TaskGroup() as tg:
            a = tg.create_task(fetch("a", 0.3))
            b = tg.create_task(fetch("b", 0.1))
    except* RuntimeError as eg:
        print("failures:", eg.exceptions)   # a was cancelled and awaited automatically
    else:
        print(a.result(), b.result())

asyncio.run(main())
```

**Why TaskGroup beats `asyncio.gather`:** with `gather(...)` the first exception propagates to the caller while the *other* tasks keep running unattended — you get work executing after your error handler, and "Task exception was never retrieved" warnings at shutdown. With `gather(..., return_exceptions=True)` you silently turn crashes into result values. `TaskGroup` guarantees no task outlives the block, aggregates every error into an `ExceptionGroup`, and is the async equivalent of `try/finally` for concurrency.

### Cancellation is cooperative

```python
async def worker(q: asyncio.Queue[int]) -> None:
    try:
        while True:
            item = await q.get()
            await handle(item)
    except asyncio.CancelledError:
        await flush_partial_state()   # cleanup
        raise                         # ALWAYS re-raise
    finally:
        await close_connection()
```

**Why re-raising is mandatory:** swallowing `CancelledError` makes the task "uncancellable"; `TaskGroup` and `asyncio.timeout` both rely on cancellation actually landing, so a task that eats it will hang the whole shutdown path. Since 3.11 `Task.cancelling()` / `Task.uncancel()` let frameworks distinguish *their* cancellation from an outer one — that is how `asyncio.timeout` converts a cancellation it caused into `TimeoutError` without stealing an outer cancel.

### Timeouts and blocking calls

```python
async def main() -> None:
    async with asyncio.timeout(2.0):          # applies to the whole block
        data = await fetch_everything()

    # Blocking / CPU-light-but-synchronous code must leave the loop thread:
    rows = await asyncio.to_thread(pandas_read_csv, "big.csv")
```

**Why `asyncio.timeout` beats `wait_for`:** `wait_for` wraps a single awaitable, so composing several sequential awaits under one deadline requires arithmetic on the remaining time. `timeout()` covers a block of arbitrary code and nests correctly. **Why `to_thread` matters:** a single blocking call (`requests.get`, `time.sleep`, a sync DB driver) stalls *every* coroutine on the loop — asyncio has no preemption.

### The fire-and-forget footgun

```python
_background: set[asyncio.Task] = set()

task = asyncio.create_task(coro())
_background.add(task)                       # keep a strong reference
task.add_done_callback(_background.discard)
```

**Why:** the event loop holds only a *weak* reference to a running task. A task nobody references can be garbage-collected mid-flight and disappear without a trace. Prefer a `TaskGroup`; use this pattern only for genuinely detached work.

## Context Variables (`contextvars`)

`contextvars.ContextVar` (PEP 567, 3.7+) provides state that is local to a *logical flow of execution* — a thread **and** an async task — instead of being global or thread-local. It is how request IDs, tenant IDs, current user, and OpenTelemetry spans propagate through modern Python services.

### Key Features:
- Each `asyncio.Task` starts with a **copy** of the context of whoever created it, so a child task can rewrite a variable without affecting its parent or siblings.
- `set()` returns a `Token`; `reset(token)` restores the previous value — the basis for safe nesting.
- `contextvars.copy_context()` snapshots the current context; `ctx.run(fn)` executes a callable inside it.
- Decimal's precision context and `asyncio`'s own machinery are built on it.

```python
import asyncio
import contextvars
from contextlib import contextmanager

request_id: contextvars.ContextVar[str] = contextvars.ContextVar("request_id", default="-")

@contextmanager
def use_request_id(value: str):
    token = request_id.set(value)
    try:
        yield
    finally:
        request_id.reset(token)      # restores the previous value, not a hardcoded default

def log(msg: str) -> None:
    print(f"[{request_id.get()}] {msg}")

async def handler(rid: str) -> None:
    with use_request_id(rid):
        log("start")
        await asyncio.sleep(0.1)     # another task runs here...
        log("end")                   # ...and our value is still ours

async def main() -> None:
    async with asyncio.TaskGroup() as tg:
        tg.create_task(handler("req-1"))
        tg.create_task(handler("req-2"))

asyncio.run(main())
# [req-1] start / [req-2] start / [req-1] end / [req-2] end
```

**Why `ContextVar` instead of a module-level global:** two concurrent requests interleave on the *same thread* in asyncio, so a global is corrupted by whichever coroutine ran last. **Why not `threading.local()`:** it is per-*thread*, and every coroutine on an event loop shares one thread — all requests would see the same slot. `ContextVar` is the only construct that is correct under threads, asyncio tasks, and generators simultaneously.

**Why `reset(token)` instead of `set(old_value)`:** the token records whether the variable was previously *unset*, so nesting restores the exact prior state rather than baking in a default.

### Gotcha: threads do not inherit context automatically

```python
ctx = contextvars.copy_context()
loop.run_in_executor(pool, lambda: ctx.run(blocking_work))   # explicit propagation
```

`asyncio.to_thread()` already copies the context for you; a raw `ThreadPoolExecutor.submit()` does **not** — the worker sees defaults. This is the usual reason request IDs vanish from logs the moment work is offloaded to a thread pool.

## Pattern Matching (Python 3.10+)
Structural pattern matching with `match` and `case` statements is a powerful feature introduced in Python 3.10. It allows for more elegant and readable code when dealing with complex data structures.

### Key Features:
- Pattern matching for sequences, mappings, and objects
- Guards and capture patterns
- Example:
```python
def process_command(command):
    match command.split():
        case ["go", direction]:
            return f"Moving {direction}"
        case ["pick", "up", item]:
            return f"Picking up {item}"
        case ["quit"]:
            return "Quitting"
        case _:
            return "Unknown command"
```

## Advanced Pattern Matching

Beyond sequence patterns, `match` supports class, mapping, or- and guard patterns. Used well it replaces long `isinstance` ladders in parsers, protocol handlers and event dispatchers.

### Key Features:
- **Class patterns** deconstruct objects positionally via `__match_args__` or by keyword via attribute names.
- **Mapping patterns** match a *subset* of keys (unlike sequence patterns, which are exhaustive) and support `**rest`.
- **Or-patterns** `|`, **guards** `if`, **as-patterns** `case Point() as p`, and value patterns via dotted names.
- `dataclasses` and `NamedTuple` generate `__match_args__` for free.

```python
from dataclasses import dataclass
from enum import Enum

@dataclass
class Click:
    x: int
    y: int

@dataclass
class KeyPress:
    key: str

class Button(Enum):
    LEFT = "left"
    RIGHT = "right"

def handle(event: object, button: Button) -> str:
    match event:
        case Click(x=0, y=0):                       # keyword deconstruction
            return "origin click"
        case Click(x, y) if x == y:                 # positional (via __match_args__) + guard
            return f"diagonal at {x}"
        case Click() as c:                          # bind the whole object
            return f"click at {c.x},{c.y}"
        case KeyPress("q" | "Q" | "esc"):           # or-pattern inside a class pattern
            return "quit"
        case {"type": "resize", "w": int(w), "h": int(h)}:   # mapping + type patterns
            return f"resize {w}x{h}"
        case {"type": str(kind), **rest}:
            return f"{kind} with extra keys {sorted(rest)}"
        case _:
            return "unknown"
```

**Why this beats an `isinstance` chain:** matching, type-checking and destructuring happen in one expression, so there is no window in which you have confirmed the type but not yet extracted the fields, and the compiler-checked structure makes a missing case visible rather than silently falling through.

### The capture-vs-compare gotcha

```python
LEFT = Button.LEFT

match button:
    case LEFT:          # BUG: bare name -> ALWAYS matches and rebinds LEFT
        ...
    case Button.LEFT:   # correct: dotted name is a *value pattern*, compared with ==
        ...
```

**Why this is the most important rule in PEP 634:** a bare identifier is a *capture pattern*, never a comparison. It matches anything and shadows the outer variable. Constants must be referenced through a dot (`Button.LEFT`, `config.MAX`, `Color.RED`) — this is a deliberate design choice that pushes enums and namespaced constants over loose module globals.

### Structural checks worth remembering

- `case [x, y]` matches any `Sequence` **except** `str`, `bytes` and `bytearray` (deliberately, so a string is not silently unpacked into characters).
- `case {"a": 1}` succeeds on `{"a": 1, "b": 2}` — mapping patterns are non-exhaustive by design; add `**rest` when you need to see the leftovers.
- Guards run only *after* the pattern matches, so `case Click(x, y) if expensive(x)` will not call `expensive()` for non-`Click` events.

## Exception Groups (Python 3.11+)
Exception Groups provide a way to handle multiple exceptions simultaneously, making error handling more robust and flexible.

### Key Features:
- Handling multiple exceptions simultaneously
- Exception group hierarchy
- `except*` syntax for handling exception groups
- Example:
```python
try:
    raise ExceptionGroup("group", [
        ValueError("invalid value"),
        TypeError("invalid type")
    ])
except* ValueError as e:
    print(f"Handled ValueError: {e}")
except* TypeError as e:
    print(f"Handled TypeError: {e}")
```

## Exception Design and Chaining

### Key Features:
- Hierarchy: `BaseException` → `Exception`, plus `KeyboardInterrupt`, `SystemExit`, `GeneratorExit` and `asyncio.CancelledError` deliberately sitting *outside* `Exception`.
- `raise New() from original` sets `__cause__` (explicit); an exception raised inside an `except` block automatically gets `__context__` (implicit).
- `raise New() from None` suppresses the chain when the inner error is an implementation detail.
- `BaseException.add_note()` (3.11+) attaches context to an exception in flight without wrapping it.

```python
class StorageError(Exception):
    """Root of everything this package raises."""

class ObjectNotFound(StorageError): ...
class StorageUnavailable(StorageError): ...

def load(key: str) -> bytes:
    try:
        return _backend.get(key)
    except KeyError as exc:
        raise ObjectNotFound(key) from exc          # __cause__: deliberate translation
    except (ConnectionError, TimeoutError) as exc:
        exc.add_note(f"while loading key={key!r}")  # 3.11+: context without wrapping
        raise StorageUnavailable(key) from exc
```

**Why a package-root exception class:** callers can write `except StorageError` and stay decoupled from whether you use S3, Redis or the filesystem underneath. Without it, every consumer must catch `KeyError`, `ConnectionError`, `botocore.ClientError`… and breaks the day you swap backends.

**Why `raise ... from exc` rather than a bare `raise MyError(...)`:** without `from`, the traceback still shows the original via `__context__` but prints "During handling of the above exception, another exception occurred", which reads like a bug in your handler. `from` prints "The above exception was the direct cause", stating that the translation was intentional. Use `from None` only when the inner exception leaks an implementation detail you do not want users to reason about.

### Never catch what you cannot handle

```python
try:
    run()
except Exception:            # correct: leaves KeyboardInterrupt/SystemExit/CancelledError alone
    log.exception("run failed")
    raise
```

**Why `except Exception` and not bare `except:`** — a bare `except` (equivalent to `except BaseException`) swallows Ctrl-C, interpreter shutdown and, in async code, `asyncio.CancelledError`, producing processes that refuse to die and tasks that cannot be cancelled. This is precisely why `CancelledError` was moved from `Exception` to `BaseException` in Python 3.8.

### Suppressing intentionally

```python
from contextlib import suppress

with suppress(FileNotFoundError):
    Path("cache.tmp").unlink()
```

**Why `suppress` beats `try/except/pass`:** it states the intent in one line at the top of the block and cannot accidentally grow a second, unrelated statement whose exceptions also get ignored — the classic way `try: ... except: pass` blocks rot.

### Python 3.14 conveniences

```python
try:
    parse(raw)
except TypeError, ValueError:        # PEP 758: parentheses now optional (when not using `as`)
    ...
```

Combine with `except*` and `ExceptionGroup` (see above) when several independent operations may fail at once — a single failure should still be raised as a plain exception, not artificially grouped.

## Type Parameter Syntax (Python 3.12+)
The new type parameter syntax provides a more intuitive way to work with generic types and type parameters.

### Key Features:
- Generic type parameters with square brackets
- Type aliases with type parameters
- Example:
```python
type List[T] = list[T]

def first[T](items: list[T]) -> T:
    return items[0]
```

## Typing Deep Dive: Protocol, TypedDict, Generics, ParamSpec

Type hints are not enforced at runtime, but for a senior they are a design tool: they encode contracts, enable refactoring at scale, and let a checker prove things tests cannot.

### Key Features:
- `Protocol` — **structural** typing ("static duck typing"); no inheritance needed.
- `TypedDict` — precise types for JSON-shaped dicts, with `Required`/`NotRequired` (3.11+) and `ReadOnly` (3.13+).
- PEP 695 (3.12+) generics: `class Box[T]:` / `def f[T](...)`, with **variance inferred automatically**.
- `Self` (3.11+), `@override` (3.12+), `ParamSpec` (3.10+), `TypeIs` (3.13+), `@overload`.

### Protocol vs ABC

```python
from typing import Protocol, runtime_checkable

@runtime_checkable
class SupportsClose(Protocol):
    def close(self) -> None: ...

def shutdown(resource: SupportsClose) -> None:
    resource.close()

shutdown(open("f.txt"))   # a file satisfies the protocol; it never imported our code
```

**Why `Protocol` over an ABC here:** an ABC requires the implementer to inherit from *your* class, which is impossible for third-party types and forces a dependency edge from library to consumer. A `Protocol` inverts that: the *consumer* declares the shape it needs, so `socket`, `file`, and a test double all qualify without modification — real dependency inversion. Keep ABCs when you also want to ship shared implementation or force registration; use `Protocol` for pure interfaces. (`@runtime_checkable` only checks method *names* at runtime, not signatures — it is a convenience, not a guarantee.)

### TypedDict for JSON boundaries

```python
from typing import TypedDict, NotRequired, ReadOnly   # ReadOnly: 3.13+

class User(TypedDict):
    id: ReadOnly[int]
    name: str
    email: NotRequired[str]

def greet(u: User) -> str:
    return f"hi {u['name']}"      # checker flags u['emial'] and u['id'] = 5
```

**Why `TypedDict` rather than `dict[str, Any]`:** you get key-name and per-key value checking with **zero runtime cost and zero shape change** — the value is still a plain `dict`, so it serialises, caches and passes to third-party libraries unchanged. Choose a `dataclass`/pydantic model instead when you need validation or behaviour.

### Modern generics and `Self`

```python
class Repository[T]:                       # PEP 695 — no TypeVar import, variance inferred
    def __init__(self) -> None:
        self._items: list[T] = []

    def add(self, item: T) -> "Self":      # `Self` types the fluent/builder pattern correctly
        self._items.append(item)
        return self
```

**Why `Self` instead of `-> Repository[T]`:** a subclass's `add()` would otherwise be typed as returning the *base* class, silently losing subclass methods for every caller of a chained API. **Why PEP 695 syntax:** the old `T = TypeVar("T", covariant=True)` made you declare variance by hand — the number one source of subtle typing bugs. In 3.12+ the checker infers it from usage.

### Decorators that keep their signature

```python
from collections.abc import Callable
from functools import wraps
import time

def timed[**P, R](fn: Callable[P, R]) -> Callable[P, R]:
    @wraps(fn)
    def inner(*args: P.args, **kwargs: P.kwargs) -> R:
        start = time.perf_counter()
        try:
            return fn(*args, **kwargs)
        finally:
            print(f"{fn.__name__}: {time.perf_counter() - start:.3f}s")
    return inner
```

**Why `ParamSpec` (`**P`) matters:** the pre-3.10 idiom `Callable[..., R]` erased the parameter list, so every decorated function accepted anything and typos in call sites went unchecked. `P.args`/`P.kwargs` forward the exact signature through the decorator.

### Narrowing helpers

```python
from typing import TypeIs, overload

def is_str_list(v: list[object]) -> TypeIs[list[str]]:
    return all(isinstance(x, str) for x in v)
```

**Why `TypeIs` (3.13+) over `TypeGuard`:** `TypeGuard` narrows only the positive branch; `TypeIs` narrows both branches (in the `else`, the checker knows the value is *not* `list[str]`), which matches how humans read the code. Use `@overload` when a function's return type depends on argument *values* (e.g. `get(key)` vs `get(key, default)`) — it is the only way to express that without returning a union the caller must re-narrow.

## Per-Interpreter GIL (Python 3.12+)
The Per-Interpreter GIL feature (PEP 684) allows for better concurrency by providing separate GILs for different interpreters.

### Key Features:
- Each subinterpreter can have its own GIL, enabling true parallelism
- Subinterpreters are "like a cross between using threads and processes"
- Extension modules must support multi-phase initialization (PEP 489) to work with per-interpreter GIL

### API Evolution:
- **Python 3.12**: Per-interpreter GIL available only through C-API
- **Python 3.13**: Basic `interpreters` module (from `test.support`)
- **Python 3.14**: Stable public API — the `concurrent.interpreters` module (PEP 734) and `InterpreterPoolExecutor` in `concurrent.futures`

### Example (Python 3.14+):
```python
from concurrent.futures import InterpreterPoolExecutor

def cpu_bound_task(n):
    return sum(i * i for i in range(n))

# Each interpreter has its own GIL - true parallelism!
with InterpreterPoolExecutor(max_workers=4) as executor:
    results = list(executor.map(cpu_bound_task, [10**6, 10**6, 10**6, 10**6]))
```

You can also manage interpreters directly:
```python
from concurrent import interpreters  # Python 3.14+

interp = interpreters.create()
interp.exec("print('hello from a subinterpreter')")
```

**Note:** For Python 3.12-3.13, you can use `from test.support import interpreters` for testing purposes, but this is not a stable public API. Since Python 3.14, use `concurrent.interpreters`.

## Free-Threaded Python (Python 3.13+, Official since 3.14)
Python 3.13 introduced an experimental free-threaded build mode (PEP 703) that completely disables the GIL, allowing true multi-threaded parallelism. In Python 3.14, free-threaded Python became **officially supported** (PEP 779) — it is no longer considered experimental, though it is still a separate build and not yet the default interpreter.

### Key Features:
- **No GIL:** Threads can run truly in parallel on multiple CPU cores
- **Officially supported since 3.14 (PEP 779):** still an optional, separate build (`--disable-gil`), shipped alongside the default build in official installers
- **Thread safety:** Uses fine-grained locking instead of the GIL
- **Compatibility:** Most pure Python code works; C extensions may need updates (the ecosystem — NumPy, and other major packages — increasingly ships free-threaded wheels)

### How to Use:
```bash
# Install free-threaded Python (e.g., via pyenv, uv or official installers)
python3.14t  # 't' suffix indicates free-threaded build

# Check if running free-threaded build
import sys
print(sys._is_gil_enabled())  # False in free-threaded build
```

### Performance Notes:
- In Python 3.13 the single-threaded overhead was significant (tens of percent); in Python 3.14 it was reduced to roughly 5-10%
- Multi-threaded CPU-bound workloads can see significant speedups
- I/O-bound code benefits less (GIL was already released during I/O)

## JIT Compiler (Python 3.13+, Experimental)
Python 3.13 added an experimental Just-In-Time (JIT) compiler (PEP 744) based on the "copy-and-patch" technique.

### Key Features:
- In Python 3.13 it had to be enabled at build time; since Python 3.14 the JIT ships in official Windows and macOS binaries, but is still **disabled by default** (enable at runtime with `PYTHON_JIT=1`)
- Modest performance improvements so far; Python 3.15 brings a significant upgrade (~8-9% geometric mean speedup on x86-64 Linux)
- Works alongside the existing specializing adaptive interpreter (PEP 659)
- Python 3.14 also added a separate **tail-calling interpreter** build option (not a JIT), giving noticeable speedups with modern compilers

## Improved Interactive Interpreter (Python 3.13+)
Python 3.13 includes a new REPL based on PyPy's, with:
- Multi-line editing with history preservation
- Color support for prompts and tracebacks
- Direct support for `help`, `exit`, `quit` without parentheses
- F1 for interactive help browsing
- Python 3.14 adds **syntax highlighting** in the REPL (enabled by default) and auto-indentation

## Platform Support (Python 3.13+)
- **iOS:** Now a PEP 11 supported platform (Tier 3)
- **Android:** Now a PEP 11 supported platform (Tier 3; official binary releases started with Python 3.14)

## Template Strings (Python 3.14+)
Template strings, or t-strings (PEP 750), use the familiar f-string syntax with a `t` prefix, but instead of producing a `str` they produce a `string.templatelib.Template` object. This gives you access to the static string parts and the interpolated values *before* they are combined, enabling safe processing (HTML escaping, SQL parameterization, structured logging, DSLs).

```python
from string.templatelib import Template, Interpolation

name = "World"
tmpl: Template = t"Hello {name}!"  # not a str!

parts = []
for item in tmpl:
    if isinstance(item, Interpolation):
        parts.append(str(item.value).upper())  # custom processing
    else:
        parts.append(item)

print("".join(parts))  # Hello WORLD!
```

Key difference from f-strings: an f-string eagerly evaluates into a plain string, while a t-string keeps structure and values separate, so a library can decide how to render them safely.

## Deferred Evaluation of Annotations (Python 3.14+)
Python 3.14 changed how type annotations work (PEP 649 and PEP 749): annotations are no longer evaluated eagerly at function/class definition time. Instead, they are stored in a special lazy form and only evaluated when accessed.

### Key Features:
- Forward references now generally work without string quotes and without `from __future__ import annotations`
- No runtime cost for annotations that are never inspected
- New `annotationlib` module for introspection, with `get_annotations()` supporting three formats: `VALUE`, `FORWARDREF`, and `STRING`

```python
class Node:
    # Works in 3.14 without quotes and without __future__ import:
    def add_child(self, child: Node) -> Node: ...

import annotationlib
annotationlib.get_annotations(Node.add_child, format=annotationlib.Format.VALUE)
```

## Other Python 3.14 Improvements
- **Zstandard compression (PEP 784):** new `compression.zstd` module in the standard library (plus `compression.*` namespaces for lzma, bz2, gzip, zlib)
- **Multiple exception types without parentheses (PEP 758):** `except TypeError, ValueError:` is now allowed (when not using `as`)
- **Zero-overhead external debugger interface (PEP 768):** attach to a running process safely, e.g. `python -m pdb -p <PID>`, and `sys.remote_exec()`
- **`map()` gained a `strict` parameter:** `map(func, a, b, strict=True)` raises if iterables have different lengths (like `zip(strict=True)`)
- **Better error messages:** continued improvements to tracebacks and suggestions
- **Color output** in `unittest`, `argparse`, `json` and `calendar` CLIs
- **Unicode 16.0.0** database
- **Improved asyncio introspection:** new CLI (`python -m asyncio ps <PID>` / `pstree <PID>`) for inspecting running async programs

## What's Coming in Python 3.15
Python 3.15 is scheduled for release in **October 2026** (currently in the release-candidate phase). Highlights:
- **Explicit lazy imports (PEP 810):** `lazy import json` — module loading is deferred until first use, improving startup time for CLIs and large applications
- **Significantly improved JIT:** ~8-9% geometric mean speedup over the standard interpreter on x86-64 Linux, ~12-13% on AArch64 macOS (over the tail-calling interpreter)
- **Tail-calling interpreter by default** in official Windows 64-bit binaries
- Continued free-threading (no-GIL) performance and ecosystem work

# Functions in Python	

## When and how many times are default arguments evaluated?

Default argument values are evaluated **once, when the `def` statement executes** — at import time for a module-level function, but on *every execution of the enclosing function* for a nested `def`. They are then stored on the function object (`f.__defaults__`) and shared between all calls.

This is why a mutable default is a classic trap:

```python
def append_to(item, target=[]):   # ONE list, created at def time, shared by all calls
    target.append(item)
    return target

append_to(1)   # [1]
append_to(2)   # [1, 2]  <- surprise

def append_to(item, target=None): # idiomatic fix: sentinel + fresh object per call
    if target is None:
        target = []
    target.append(item)
    return target
```

**Why the sentinel idiom is preferred:** the default is now created inside the call, so every invocation gets a fresh list, while the signature still documents that the argument is optional. (Note: `dataclasses` refuses mutable defaults outright and makes you use `field(default_factory=list)` for the same reason.)

## `partial`

`functools.partial(func, /, *args, **keywords)`

Return a new partial object which when called will behave like func called with the positional arguments args and keyword arguments keywords. If more arguments are supplied to the call, they are appended to args. If additional keyword arguments are supplied, they extend and override keywords.

## `functools` Deep Dive: Caching, Dispatch, Ordering

### Key Features:
- `@cache` (3.9+) — unbounded memoisation; `@lru_cache(maxsize=N)` — bounded.
- `@cached_property` — computed once per *instance*, stored in the instance `__dict__`.
- `@singledispatch` / `@singledispatchmethod` — type-based dispatch without `isinstance` chains.
- `@total_ordering`, `reduce`, `partial`, `wraps`.

```python
from functools import cache, cached_property, singledispatch, total_ordering

@cache                                   # no maxsize bookkeeping -> faster than lru_cache(None)
def fib(n: int) -> int:
    return n if n < 2 else fib(n - 1) + fib(n - 2)

fib(200)
fib.cache_info()      # CacheInfo(hits=..., misses=201, maxsize=None, currsize=201)
fib.cache_clear()
```

**Why `@cache` over a hand-rolled dict:** you get `cache_info()` for hit-rate observability and `cache_clear()` for test isolation for free, and the lookup is implemented in C. **Why `@lru_cache(maxsize=...)` instead of `@cache` in a service:** `@cache` never evicts, so caching on user-controlled input is an unbounded memory leak. Arguments must also be hashable, and `f(1)` and `f(n=1)` are cached as *different* keys.

### The `lru_cache`-on-methods trap

```python
class Client:
    @cache                                  # BUG: `self` becomes part of the cache key
    def lookup(self, key: str) -> str: ...
```

**Why this leaks:** the cache lives on the *class* and holds a strong reference to every `self` ever passed, so no `Client` instance is ever collected. Cache a module-level function that takes only the hashable inputs, or use `@cached_property` for per-instance memoisation.

### `cached_property`

```python
class Report:
    def __init__(self, rows: list[dict]) -> None:
        self.rows = rows

    @cached_property
    def totals(self) -> dict[str, float]:
        print("computing...")            # runs once per instance
        return aggregate(self.rows)
```

**Why it is better than `@property` + a `self._totals` guard:** it removes the sentinel-checking boilerplate and, because it is a *non-data* descriptor, subsequent accesses bypass the descriptor entirely and read straight from `self.__dict__` — zero call overhead after the first hit. Two caveats worth stating in an interview: it needs a `__dict__` (so it is incompatible with `__slots__`), and **since Python 3.12 the internal class-wide lock was removed** — concurrent first accesses may each compute the value (one wins), which fixed a serious contention bottleneck but means the function must be side-effect-free.

### `singledispatch` instead of isinstance ladders

```python
@singledispatch
def render(value: object) -> str:
    raise TypeError(f"cannot render {type(value).__name__}")

@render.register
def _(value: int) -> str: return f"{value:,}"

@render.register
def _(value: list) -> str: return ", ".join(render(v) for v in value)
```

**Why:** new types register themselves from *their own* module — you extend behaviour without editing the original function, which is the Open/Closed principle applied to functions. Dispatch respects the MRO, so registering `Sequence` covers subclasses automatically. Use `@singledispatchmethod` for the same effect on methods (it dispatches on the *second* argument, since the first is `self`).

### `total_ordering`

```python
@total_ordering
class Version:
    def __init__(self, parts: tuple[int, ...]) -> None: self.parts = parts
    def __eq__(self, other): return self.parts == other.parts
    def __lt__(self, other): return self.parts < other.parts
```

**Why:** define `__eq__` + one ordering method and get the other three derived. Hand-written comparison methods are where inconsistent orderings (`a < b` and `b < a` both true) hide. The cost is a small performance penalty per comparison — define all six by hand only in a proven hot path.

## Best practice decorators for functions

The basic idea is to use a function, but return a partial object of itself if it is called with parameters before being used as a decorator:

```python
from functools import wraps, partial

def decorator(func=None, parameter1=None, parameter2=None):

   if not func:
        # The only drawback is that for functions there is no thing
        # like "self" - we have to rely on the decorator 
        # function name on the module namespace
        return partial(decorator, parameter1=parameter1, parameter2=parameter2)
   @wraps(func)
   def wrapper(*args, **kwargs):
        # Decorator code-  parameter1, etc... can be used 
        # freely here
        return func(*args, **kwargs)
   return wrapper
```
And that is it - decorators written using this pattern can decorate a function right away without being "called" first:
```python
@decorator
def my_func():
    pass
```
Or customized with parameters:

```python
@decorator(parameter1="example.com", ...):
def my_func():
    pass
```

## Decorator

```python
import functools

def require_authorization(f):
    @functools.wraps(f)
    def decorated(user, *args, **kwargs):
        if not is_authorized(user):
            raise UserIsNotAuthorized
        return f(user, *args, **kwargs)
    return decorated

@require_authorization
def check_email(user, etc):
    # etc.
```

## Decorator factory (passing args to decorators)

```python
def require_authorization(action):
    def decorate(f):
        @functools.wraps(f)
        def decorated(user, *args, **kwargs):
            if not is_allowed_to(user, action):
                raise UserIsNotAuthorized(action, user)
            return f(user, *args, **kwargs)
        return decorated
    return decorate
```

## `wraps`

`functools.wraps` copies the wrapped function's metadata onto the wrapper: `__module__`, `__name__`, `__qualname__`, `__doc__`, `__dict__`, and sets `__wrapped__` pointing back to the original. The `__wrapped__` attribute is what lets `inspect.signature()` and debuggers see through the decorator. Without `wraps`, every decorated function reports the wrapper's name and signature, which breaks introspection, documentation tools, and pickling.

## Decorator for class
1. Just use inheritance
2. Use decorator, that returns class
```python
def addID(original_class):
    orig_init = original_class.__init__
    # Keep a reference to the original __init__, so we can call it without recursion

    def __init__(self, id, *args, **kws):
        self._id = id
        orig_init(self, *args, **kws)  # Call the original __init__

    def get_id(self):
        return self._id

    original_class.__init__ = __init__  # Replace the class' __init__ with the new one
    original_class.get_id = get_id
    return original_class

@addID
class Foo:
    pass

Foo(42).get_id()   # 42
```
3. Use metaclass

Indeed, metaclasses are especially useful to do black magic, and therefore complicated stuff. But by themselves, they are simple:

* intercept a class creation
* modify the class
* return the modified class

```python
>>> class Foo(object):
...       bar = True

>>> Foo = type('Foo', (), {'bar':True})

class UpperAttrMetaclass(type):
    def __new__(cls, clsname, bases, attrs):
        uppercase_attrs = {
            attr if attr.startswith("__") else attr.upper(): v
            for attr, v in attrs.items()
        }
        return super().__new__(cls, clsname, bases, uppercase_attrs)
```

Note: returning `type(clsname, bases, uppercase_attrs)` instead of `super().__new__(...)` is a classic bug — the produced class would be an instance of plain `type`, not of the metaclass, so the metaclass would not apply to subclasses.

The main use case for a metaclass is creating an API. A typical example of this is the Django ORM.

## Indirect function calls
1) use another variable for this function
2) use `partial`
3) use as parameter `def indirect(func, *args)`
4) use nested func and return it (functional approach)
5) `eval("func_name()")` -> returns func result
6) `exec("func_name()")` -> returns None
7) importing module (assuming module foo with method bar):
```python
module = __import__('foo')
func = getattr(module, 'bar')
func()
```
8) `locals()["myfunction"]()`
9) `globals()["myfunction"]()`
10) dict()
```python
functions = {'myfoo': foo.bar}

mystring = 'myfoo'
if mystring in functions:
    functions[mystring]()
```

## Function introspection

Introspection is an ability to determine the type of an object at runtime. Everything in python is an object. Every object in Python may have attributes and methods. By using introspection, we can dynamically examine python objects. Code Introspection is used for examining the classes, methods, objects, modules, keywords and get information about them so that we can utilize it. Introspection reveals useful information about your program's objects. 

- `type()`: This function returns the type of an object.
- `dir()`: This function return list of methods and attributes associated with that object.
- `id()`: This function returns a special id of an object.
- `help()`	It is used it to find what other functions do
- `hasattr()`	Checks if an object has an attribute
- `getattr()`	Returns the contents of an attribute if there are some.
- `repr()`	Return string representation of object
- `callable()`	Checks if an object is a callable object (a function)or not.
- `issubclass()`	Checks if a specific class is a derived class of another class.
- `isinstance()`	Checks if an objects is an instance of a specific class.
- `sys()`	Give access to system specific variables and functions
- `__doc__`	Return some documentation about an object
- `__name__`	Return the name of the object.

## Implementation details of functional programming, for vs map
Functional programming is a programming paradigm in which the primary method of computation is evaluation of pure functions. Although Python is not primarily a functional language, it's good to be familiar with `lambda`, `map()`, `filter()`, and `reduce()` because they can help you write concise, high-level, parallelizable code. You'll also see them in code that others have written.

```python
list(
     map(
         (lambda a, b, c: a + b + c),
         [1, 2, 3],
         [10, 20, 30],
         [100, 200, 300]
     )
)
list(filter(lambda s: s.isupper(), ["cat", "Cat", "CAT", "dog", "Dog", "DOG", "emu", "Emu", "EMU"]))
reduce(lambda x, y: x + y, [1, 2, 3, 4, 5], 100)  # (100 + 1 + 2 + 3 + 4 + 5), 100 is initial value
```


## Function attributes
```python
def func():
    pass
dir(func)
    Out[3]: 
    ['__annotations__',
     '__call__',
    ...
     '__str__',
     '__subclasshook__']
func.a = 1
dir(func)
    Out[5]: 
    ['__annotations__',
     '__call__',
    ...
     '__str__',
     '__subclasshook__',
     'a']
print(func.__dict__)
{'a': 1}
func.__getattribute__("a")
    Out[7]: 1
```

# Scopes in Python	
## LEGB rule

Python resolves names using the so-called LEGB rule, which is named after the Python scope for names. The letters in LEGB stand for Local, Enclosing, Global, and Built-in. Here's a quick overview of what these terms mean:

1. Local (or function) scope is the code block or body of any Python function or lambda expression. This Python scope contains the names that you define inside the function. These names will only be visible from the code of the function. It's created at function call, not at function definition, so you'll have as many different local scopes as function calls. This is true even if you call the same function multiple times, or recursively. Each call will result in a new local scope being created.

2. Enclosing (or nonlocal) scope is a special scope that only exists for nested functions. If the local scope is an inner or nested function, then the enclosing scope is the scope of the outer or enclosing function. This scope contains the names that you define in the enclosing function. The names in the enclosing scope are visible from the code of the inner and enclosing functions.

3. Global (or module) scope is the top-most scope in a Python program, script, or module. This Python scope contains all of the names that you define at the top level of a program or a module. Names in this Python scope are visible from everywhere in your code. `dir()`

4. Built-in scope is a special Python scope that's created or loaded whenever you run a script or open an interactive session. This scope contains names such as keywords, functions, exceptions, and other attributes that are built into Python. Names in this Python scope are also available from everywhere in your code. It's automatically loaded by Python when you run a program or script. `dir(__builtins__)`: 152 names

The LEGB rule is a kind of name lookup procedure, which determines the order in which Python looks up names. For example, if you reference a given name, then Python will look that name up sequentially in the local, enclosing, global, and built-in scope. If the name exists, then you'll get the first occurrence of it. Otherwise, you'll get an error.

When you call `dir()` with no arguments, you get the list of names available in your main global Python scope. Note that if you assign a new name (like var here) at the top level of the module (which is `__main__` here), then that name will be added to the list returned by `dir()`.

## `global` and `nonlocal`

### The `global` Statement

The statement consists of the global keyword followed by one or more names separated by commas. You can also use multiple global statements with a name (or a list of names). All the names that you list in a global statement will be mapped to the global or module scope in which you define them.

### The `nonlocal` Statement
Similarly to global names, nonlocal names can be accessed from inner functions, but not assigned or updated. If you want to modify them, then you need to use a nonlocal statement. With a nonlocal statement, you can define a list of names that are going to be treated as nonlocal.

The nonlocal statement consists of the nonlocal keyword followed by one or more names separated by commas. These names will refer to the same names in the enclosing Python scope. 

## Scopes and nested functions, closures

This technique by which some data (hello in this case) gets attached to the code is called closure in Python.

```python
def print_msg(msg):
    # This is the outer enclosing function
    def printer():
        # This is the nested function
        print(msg)
    return printer  # returns the nested function

# Now let's try calling this function.
another = print_msg("Hello")
another()
# Output: Hello
```

The criteria that must be met to create closure in Python are summarized in the following points.

- We must have a nested function (function inside a function).
- The nested function must refer to a value defined in the enclosing function.
- The enclosing function must return the nested function.

Python Decorators make an extensive use of closures as well.

## globals() и locals(): Meaning, could we change both of them?	

- `globals()` always returns the dictionary of the module namespace
- `locals()` always returns a dictionary of the current namespace
- `vars()` returns either a dictionary of the current namespace (if called with no argument) or the dictionary of the argument.

It does not automatically update when variables are assigned, and assigning entries in the dict will not assign the corresponding local variables.

# Modules in Python		

## Module `reload`, `importlib`

Reload a previously imported module. The argument must be a module object, so it must have been successfully imported before. This is useful if you have edited the module source file using an external editor and want to try out the new version without leaving the Python interpreter. The return value is the module object (which can be different if re-importing causes a different object to be placed in sys.modules).

```python
from importlib import reload  # Python 3.4+
import foo

while True:
    # Do some things.
    if is_changed(foo):
        foo = reload(foo)
```

# OOP in Python	

## SOLID
In software engineering, SOLID is a mnemonic acronym for five design principles intended to make software designs more understandable, flexible, and maintainable. The principles are a subset of many principles promoted by American software engineer and instructor Robert C. Martin, first introduced in his 2000 paper Design Principles and Design Patterns.

The SOLID ideas are

- The single-responsibility principle: "There should never be more than one reason for a class to change." In other words, every class should have only one responsibility.
- The open–closed principle: "Software entities ... should be open for extension, but closed for modification."
- The Liskov substitution principle: "Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it." See also design by contract.
- The interface segregation principle: "Many client-specific interfaces are better than one general-purpose interface."
- The dependency inversion principle: "Depend upon abstractions, not concretions."

The SOLID acronym was introduced later, around 2004, by Michael Feathers.

## The four basics of object-oriented programming

- Encapsulation - binding the data and functions which operate on that data into a single unit, the class

- Abstraction - treating a system as a "black box," where it's not important to understand the gory inner workings in order to reap the benefits of using it.

- Inheritance - if a class inherits from another class, it automatically obtains a lot of the same functionality and properties from that class and can be extended to contain separate code and data. A nice feature of inheritance is that it often leads to good code reuse since a parent class' functions don't need to be re-defined in any of its child classes.

- Polymorphism - Because derived objects share the same interface as their parents, the calling code can call any function in that class' interface. At run-time, the appropriate function will be called depending on the type of object passed leading to possibly different behaviors.


## abstract base class

They make sure that derived classes implement methods and properties dictated in the abstract base class.
Abstract base classes separate the interface from the implementation. They define generic methods and properties that must be used in subclasses. Implementation is handled by the concrete subclasses where we can create objects that can handle tasks.
They help to avoid bugs and make the class hierarchies easier to maintain by providing a strict recipe to follow for creating subclasses.

```python
from abc import ABCMeta, abstractmethod

class AbstactClassCSV(metaclass = ABCMeta):  # or just inherits from ABC, helper class
    def __init__(self, path, file_name):
       self._path = path
       self._file_name = file_name
        
    @property
    @abstractmethod
    def path(self):
       pass  
```

## getattr(), setattr()

`hasattr(object, name)` function:

Determines whether an object has a name attribute or a name method, returns a bool value, returns True with a name attribute, or returns False.

`getattr(object, name[,default])` function:

Gets the property or method of the object, prints it if it exists, or prints the default value if it does not exist, which is optional.

`setattr(object, name, values)` function:

Assign a value to an object's property. If the property does not exist, create it before assigning it.

## `__getattr__`, `__setattr__`, `__delattr__`

```python
>>> # this example uses __setattr__ to dynamically change attribute value to uppercase
>>> class Frob:
...     def __setattr__(self, name, value):
...         self.__dict__[name] = value.upper()
...
>>> f = Frob()
>>> f.bamf = "bamf"
>>> f.bamf
'BAMF'
```

Note that if the attribute is found through the normal mechanism, `__getattr__()` is not called. (This is an intentional asymmetry between `__getattr__()` and `__setattr__()`.) This is done both for efficiency reasons and because otherwise `__getattr__()` would have no way to access other attributes of the instance.

```python
>>> class Frob:
...     def __init__(self, bamf):
...         self.bamf = bamf
...     def __getattr__(self, name):
...         return 'Frob does not have `{}` attribute.'.format(str(name))
...
>>> f = Frob("bamf")
>>> f.bar
'Frob does not have `bar` attribute.'
>>> f.bamf
'bamf'
```


## `__getattribute__`

If the class also defines `__getattr__()`, the latter will not be called unless `__getattribute__()` either calls it explicitly or raises an AttributeError.

```python
>>> class Frob(object):
...     def __getattribute__(self, name):
...         print(f"getting `{name}`")
...         return object.__getattribute__(self, name)
...
>>> f = Frob()
>>> f.bamf = 10
>>> f.bamf
getting `bamf`
10
```

## Name mangling

In the name mangling process, any identifier with **two or more leading underscores and at most one trailing underscore** is textually replaced with `_classname__identifier`, where classname is the current class name with leading underscore(s) stripped. So `__geek` and `__geek_` are mangled, while dunders like `__geek__` are **not** (that's why `__init__` works unmangled). Mangling happens at compile time inside the class body only — its purpose is to avoid accidental clashes in subclasses, not to provide real privacy.

```python
class Student:
    def __init__(self, name):
        self.__name = name
  
s1 = Student("Santhosh")
print(s1._Student__name)
```

## @property(getter, setter, deleter)

```python
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        print('Getting name')
        return self._name

    @name.setter
    def name(self, value):
        print('Setting name to ' + value)
        self._name = value

    @name.deleter
    def name(self):
        print('Deleting name')
        del self._name

p = Person('Adam')
print('The name is:', p.name)
p.name = 'John'
del p.name
```

## Descriptor Protocol

A **descriptor** is any object that defines `__get__`, `__set__` or `__delete__` and is stored **as a class attribute**. Descriptors are the mechanism behind `property`, `classmethod`, `staticmethod`, `functools.cached_property`, and every ORM field you have ever used — understanding them means you stop writing five nearly-identical properties per class.

### Key Features:
- **Data descriptor** — defines `__set__` and/or `__delete__`. Takes priority *over* the instance `__dict__`.
- **Non-data descriptor** — defines only `__get__`. The instance `__dict__` wins over it.
- Attribute lookup order in `object.__getattribute__`: **type data descriptor → instance `__dict__` → type non-data descriptor / plain class attribute → `__getattr__`**.
- `__set_name__(self, owner, name)` (3.6+) is called automatically at class creation, so a descriptor learns the attribute name it was assigned to — no more `Field("price")` duplication.

```python
class Positive:
    """One reusable validator instead of a hand-written property per field."""

    def __set_name__(self, owner: type, name: str) -> None:
        self._name = f"_{name}"          # storage slot on the instance

    def __get__(self, obj, objtype=None):
        if obj is None:                  # accessed on the class: Order.price
            return self
        return getattr(obj, self._name)

    def __set__(self, obj, value: float) -> None:
        if value <= 0:
            raise ValueError(f"{self._name[1:]} must be positive, got {value!r}")
        setattr(obj, self._name, value)  # plain attribute -> no recursion


class Order:
    quantity = Positive()
    price = Positive()

    def __init__(self, quantity: int, price: float) -> None:
        self.quantity = quantity   # routed through Positive.__set__
        self.price = price

Order(1, -5)   # ValueError: price must be positive, got -5
```

**Why this is better than three `@property` blocks:** the validation rule lives in exactly one place. Adding a tenth validated field costs one line, and `__set_name__` removes the string-duplication bug where a copy-pasted property writes to the wrong backing attribute.

### `property` demystified

`property` is *just* a data descriptor written in C. A minimal pure-Python equivalent:

```python
class my_property:
    def __init__(self, fget): self.fget = fget
    def __get__(self, obj, objtype=None):
        return self if obj is None else self.fget(obj)
    def __set__(self, obj, value):
        raise AttributeError("read-only")   # having __set__ is what makes it a data descriptor
```

**Why the distinction matters:** because `property` defines `__set__`, you cannot shadow it by writing to `instance.__dict__` — assignment always goes through the setter. `functools.cached_property` deliberately omits `__set__`, so after the first call it writes the computed value into the instance `__dict__` and every later access hits the *dict*, not the descriptor. That is the entire caching trick, and it is also why `cached_property` cannot be used on a class with `__slots__` (no `__dict__` to cache into).

### Functions are non-data descriptors

```python
class A:
    def method(self): ...

A.method            # plain function
A().method          # <bound method A.method of ...>  <- function.__get__ produced this
A.__dict__["method"].__get__(A(), A)   # exactly what attribute access does
```

**Why you should know this:** bound methods are not stored anywhere — they are created on every attribute access by `function.__get__`. That explains why `self` is passed implicitly, why `staticmethod` (which returns the underlying function unchanged) exists, and why storing `obj.method` in a long-lived callback list keeps `obj` alive.

## init,  repr, str, cmp,  new , del,  hash, nonzero, unicode, class operators

- `__init__` The task of constructors is to initialize(assign values) to the data members of the class when an object of class is created.
- `repr()` The repr() function returns a printable representation of the given object.
- The `__str__` method in Python represents the class objects as a string – it can be used for classes. The __str__ method should be defined in a way that is easy to read and outputs all the members of the class. This method is also used as a debugging tool when the members of a class need to be checked.
- `__cmp__` is no longer used.
- `__new__` Whenever a class is instantiated `__new__` and `__init__` methods are called. `__new__` method will be called when an object is created and `__init__` method will be called to initialize the object.
```python
class A(object):
    def __new__(cls):
         print("Creating instance")
         return super(A, cls).__new__(cls)
  
    def __init__(self):
        print("Init is called")
```
Output:

- Creating instance
- Init is called

- `__del__` The `__del__()` method is a known as a destructor method in Python. It is called when all references to the object have been deleted i.e when an object is garbage collected. Note : A reference to objects is also deleted when the object goes out of reference or when the program ends
- `__hash__()`
```python
class A(object):

    def __init__(self, a, b, c):
        self._a = a
        self._b = b
        self._c = c

    def __eq__(self, othr):
        return (isinstance(othr, type(self))
                and (self._a, self._b, self._c) ==
                    (othr._a, othr._b, othr._c))

    def __hash__(self):
        return hash((self._a, self._b, self._c))
```

## Rich comparison methods

`__lt__`, `__gt__`, `__le__`, `__ge__`, `__eq__`, and `__ne__`

```python
def __lt__(self, other):
   ...
def __le__(self, other):
   ...
def __gt__(self, other):
   ...
def __ge__(self, other):
   ...
def __eq__(self, other):
   ...
def __ne__(self, other):
   ...
```

## `__call__`

`object()` is shorthand for `object.__call__()`

```python
class Product:
    def __init__(self):
        print("Instance Created")
  
    # Defining __call__ method
    def __call__(self, a, b):
        print(a * b)
  
# Instance created
ans = Product()
  
# __call__ method will be called
ans(10, 20)
```

## Multiple inheritance

Python has known at least three different MRO algorithms: classic, Python 2.2 new-style, and Python 2.3 new-style (a.k.a. C3). Only the latter survives in Python 3.

## Classic algorithm

Classic classes used a simple MRO scheme: when looking up a method, base classes were searched using a simple depth-first left-to-right scheme. The first matching object found during this search would be returned. For example, consider these classes:
```python
class A:
  def save(self): pass

class B(A): pass

class C:
  def save(self): pass

class D(B, C): pass
```
If we created an instance x of class D, the classic method resolution order would order the classes as D, B, A, C. Thus, a search for the method x.save() would produce A.save() (and not C.save()). 

## Diamond problem

One problem concerns method lookup under "diamond inheritance." For example:
```python
class A:
  def save(self): pass

class B(A): pass

class C(A):
  def save(self): pass

class D(B, C): pass
```
Here, class D inherits from B and C, both of which inherit from class A. Using the classic MRO, methods would be found by searching the classes in the order D, B, A, C, A. Thus, a reference to x.save() will call A.save() as before. However, this is unlikely what you want in this case! Since both B and C inherit from A, one can argue that the redefined method C.save() is actually the method that you want to call, since it can be viewed as being "more specialized" than the method in A (in fact, it probably calls A.save() anyways). For instance, if the save() method is being used to save the state of an object, not calling C.save() would break the program since the state of C would be ignored.

Although this kind of multiple inheritance was rare in existing code, new-style classes would make it commonplace. This is because all new-style classes were defined by inheriting from a base class object. Thus, any use of multiple inheritance in new-style classes would always create the diamond relationship described above. For example:
````python
class B(object): pass

class C(object):
  def __setattr__(self, name, value): pass

class D(B, C): pass
````

Moreover, since object defined a number of methods that are sometimes extended by subtypes (e.g., __setattr__()), the resolution order becomes critical. For example, in the above code, the method C.__setattr__ should apply to instances of class D.

To fix the method resolution order for new-style classes in Python 2.2, G. adopted a scheme where the MRO would be pre-computed when a class was defined and stored as an attribute of each class object. The computation of the MRO was officially documented as using a depth-first left-to-right traversal of the classes as before. If any class was duplicated in this search, all but the last occurrence would be deleted from the MRO list. So, for our earlier example, the search order would be D, B, C, A (as opposed to D, B, A, C, A with classic classes).

In reality, the computation of the MRO was more complex than this. Guido discovered a few cases where this new MRO algorithm didn't seem to work. Thus, there was a special case to deal with a situation when two bases classes occurred in a different order in the inheritance list of two different derived classes, and both of those classes are inherited by yet another class. For example:
```python
class A(object): pass
class B(object): pass
class X(A, B): pass
class Y(B, A): pass
class Z(X, Y): pass
```
Using the tentative new MRO algorithm, the MRO for these classes would be Z, X, Y, B, A, object. (Here 'object' is the universal base class.) However, I didn't like the fact that B and A were in reversed order. Thus, the real MRO would interchange their order to produce Z, X, Y, A, B, object.


## MRO, super

Thus, in Python 2.3, we abandoned my home-grown 2.2 MRO algorithm in favor of the academically vetted C3 algorithm. One outcome of this is that Python will now reject any inheritance hierarchy that has an inconsistent ordering of base classes. For instance, in the previous example, there is an ordering conflict between class X and Y. For class X, there is a rule that says class A should be checked before class B. However, for class Y, the rule says that class B should be checked before A. In isolation, this discrepancy is fine, but if X and Y are ever combined together in the same inheritance hierarchy for another class (such as in the definition of class Z), that class will be rejected by the C3 algorithm. This, of course, matches the Zen of Python's "errors should never pass silently" rule.

**In Python, the MRO is from bottom to top and left to right. This means that, first, the method is searched in the class of the object. If it's not found, it is searched in the immediate super class. In the case of multiple super classes, it is searched left to right, in the order by which was declared by the developer. For example:**

## Mixins

A mixin is a special kind of multiple inheritance. There are two main situations where mixins are used:

- You want to provide a lot of optional features for a class.
- You want to use one particular feature in a lot of different classes.

## metaclass definition

Metaclasses are the 'stuff' that creates classes.

You define classes in order to create objects, right?

But we learned that Python classes are objects.

Well, metaclasses are what create these objects. They are the classes' classes, you can picture them this way:

```python
MyClass = MetaClass()
my_object = MyClass()

# You've seen that type lets you do something like this:

MyClass = type('MyClass', (), {})
```

## `__init_subclass__`, `__set_name__`, `__class_getitem__`

PEP 487 added two hooks that cover most of what people used to write metaclasses for — with none of the metaclass-conflict problems.

### Key Features:
- `__init_subclass__(cls, **kwargs)` — implicitly a classmethod; runs on the **subclass** at class-creation time. Accepts keyword arguments passed in the class header.
- `__set_name__(self, owner, name)` — called on every class-body attribute that defines it, right after the class is created.
- `__class_getitem__(cls, item)` — makes `MyClass[int]` valid, powering generic aliases.

### Subclass registration and validation without a metaclass

```python
class Plugin:
    registry: dict[str, type["Plugin"]] = {}

    def __init_subclass__(cls, /, name: str | None = None, abstract: bool = False, **kw):
        super().__init_subclass__(**kw)          # cooperative: never break the chain
        if abstract:
            return
        if not hasattr(cls, "run"):
            raise TypeError(f"{cls.__name__} must define run()")
        Plugin.registry[name or cls.__name__.lower()] = cls


class Csv(Plugin, name="csv"):
    def run(self) -> None: ...

class Broken(Plugin):          # TypeError raised at import time, not at first use
    pass
```

**Why this beats a metaclass:** a metaclass changes the *type* of the class, so any class combining two libraries that each ship a metaclass hits `TypeError: metaclass conflict`. `__init_subclass__` is a plain hook on a normal class — it composes freely via `super()`, is readable to anyone who knows classmethods, and still gives you the two things metaclasses were used for: registration and structural validation at import time (fail fast, not on first request).

**Why `super().__init_subclass__(**kw)` is mandatory:** several classes in an MRO may each define the hook; skipping the `super()` call silently disables every one below yours.

### `__set_name__` for self-naming attributes

```python
class Field:
    def __set_name__(self, owner: type, name: str) -> None:
        self.name = name
        self.owner = owner

class Model:
    title = Field()      # title.name == "title", no string duplication
```

**Why:** before 3.6 a descriptor could not know its own name, so every ORM/serialiser made you write `title = Field("title")` — a permanent source of copy-paste bugs where the label and the attribute drifted apart. The hook also receives `owner`, which lets an attribute register itself with the class that contains it.

### `__class_getitem__` for subscriptable classes

```python
from types import GenericAlias

class Result:
    def __class_getitem__(cls, item):
        return GenericAlias(cls, item)      # Result[int] is now a valid annotation

def parse(raw: str) -> Result[int]: ...
```

**Why return `types.GenericAlias` rather than just `cls`:** the alias preserves the parameter for introspection (`__origin__`/`__args__`), so `typing.get_type_hints` and runtime validators can read it. In practice, inheriting `Generic[T]` — or, in 3.12+, simply writing `class Result[T]:` — does this for you; implement `__class_getitem__` by hand only for non-generic runtime factories such as `Annotated`-style DSLs.

## type(), isinstance(), issubclass()

### `type()` Parameters
The `type()` function either takes a single object parameter.

Or, it takes 3 parameters

`name` - a class name; becomes the `__name__` attribute
`bases` - a tuple that itemizes the base class; becomes the `__bases__` attribute
`dict` - a dictionary which is the namespace containing definitions for the class body; becomes the `__dict__` attribute

### `type()` Return Value
The `type()` function returns

type of the object, if only one object parameter is passed
a new type, if 3 parameters passed

The isinstance() function returns True if the specified object is of the specified type, otherwise False.

If the type parameter is a tuple, this function will return True if the object is one of the types in the tuple.

The issubclass() function checks if the class argument (first argument) is a subclass of classinfo class (second argument).

The syntax of issubclass() is:

`issubclass(class, classinfo)`

## `__slots__`	

The special attribute `__slots__` allows you to explicitly state which instance attributes you expect your object instances to have, with the expected results:

- **space savings in memory** — the dominant, measurable win (roughly half the size per instance): value references are stored in fixed slots instead of a per-instance `__dict__`.
- slightly faster attribute access.

```python
class Base:
    __slots__ = 'foo', 'bar'

class Right(Base):
    __slots__ = 'baz', 
```

### Caveats worth knowing:
- **No `__dict__`** → no ad-hoc attributes at runtime, and `functools.cached_property` does not work (it needs a `__dict__` to cache into).
- **A subclass that omits `__slots__` silently regains `__dict__`**, erasing the memory savings for the whole hierarchy — every class in the chain must declare slots.
- **Multiple inheritance from two classes with non-empty slots raises `TypeError`** (conflicting instance layouts).
- **`__weakref__` must be declared explicitly** in `__slots__` if you need weak references to instances.
- With dataclasses, use `@dataclass(slots=True)` (3.10+) instead of writing `__slots__` by hand.

## dataclasses vs NamedTuple vs TypedDict

Picking the right record type is a daily senior decision. All four options below generate boilerplate for you; they differ in mutability, memory, and whether validation happens.

| | `@dataclass` | `NamedTuple` | `TypedDict` | pydantic `BaseModel` |
|---|---|---|---|---|
| Runtime type | new class | `tuple` subclass | plain `dict` | new class |
| Mutable | yes (`frozen=True` opts out) | no | yes | yes |
| Validates input | **no** | no | no | **yes** |
| Iterable / unpackable | no | yes | keys only | no |
| Memory | low (`slots=True`) | lowest | dict-sized | highest |
| Best for | domain objects, config | fixed coordinate-like records, hot loops | JSON at API boundaries | untrusted external input |

```python
from dataclasses import dataclass, field, replace

@dataclass(slots=True, frozen=True, kw_only=True)
class Money:
    amount: int
    currency: str = "USD"
    tags: list[str] = field(default_factory=list)   # never `tags: list = []`

m = Money(amount=100)
m2 = replace(m, amount=200)     # copy.replace(m, amount=200) also works in 3.13+
```

**Why `slots=True` (3.10+):** it removes the per-instance `__dict__`, cutting memory roughly in half and speeding up attribute access — the single highest-value flag for objects you create in bulk. **Why `frozen=True`:** immutable instances are hashable and safe to share across threads and caches; mutation becomes an explicit `replace()`, which makes accidental aliasing bugs impossible. **Why `kw_only=True` (3.10+):** positional construction of a 6-field record is unreadable and silently breaks when you reorder fields; it also removes the "non-default argument follows default argument" restriction. **Why `field(default_factory=list)`:** a bare `[]` default would be evaluated once at class-definition time and shared by every instance — the same trap as mutable default arguments (dataclasses actually raise `ValueError` for this, unlike plain functions).

```python
from typing import NamedTuple

class Point(NamedTuple):
    x: float
    y: float

px, py = Point(1.0, 2.0)      # unpacks like a tuple; works in match statements
```

**Why `NamedTuple` over a frozen dataclass:** it *is* a tuple, so it unpacks, indexes, compares structurally, and is the cheapest option in a tight loop. **Why that is also its weakness:** because `Point(1, 2) == (1, 2)` is `True`, a `NamedTuple` silently compares equal to unrelated tuples and can be passed where a plain tuple is expected — accidental coupling a dataclass would have caught.

### Where validation belongs

`@dataclass` performs **no** type checking: `Money(amount="oops")` constructs happily. That is correct for data you produced yourself, and wrong for data crossing a trust boundary.

**Rule of thumb:** parse untrusted input (HTTP bodies, config files, message payloads) with a validating model — pydantic v2, whose core is in Rust and is typically an order of magnitude faster than v1 — then convert to plain dataclasses for your domain layer. `attrs` remains the richest option (validators, converters, `__attrs_post_init__`) and is what `dataclasses` was distilled from; reach for it when you need per-field converters that stdlib dataclasses do not provide. Keeping validation at the edge means the core of your application never re-checks the same invariants.

# Troubleshooting in Python	
## Types of profilers: Static and dynamic profilers

Serious software development calls for performance optimization. When you start optimizing application performance, you can't escape looking at profilers. Whether monitoring production servers or tracking frequency and duration of method calls, profilers run the gamut

### `trace` module

You can do several things with trace:

1. Produce a code coverage report to see which lines are run or skipped over (`python3 -m trace –count trace_example/main.py`).
2. Report on the relationships between functions that call one other (`python3 -m trace –listfuncs trace_example/main.py | grep -v importlib`).
3. Track which function is the caller (`python3 -m trace –listfuncs –trackcalls trace_example/main.py | grep -v importlib`).

### `faulthandler` module

By contrast, faulthandler has slightly better Python documentation. It states that its purpose is to dump Python tracebacks explicitly on a fault, after a timeout, or on a user signal. It also works well with other system fault handlers like Apport or the Windows fault handler. Both the faulthandler and trace modules provide more tracing abilities and can help you debug your Python code. For more profiling statistics, see the next section.

If you're a beginner to tracing, I recommend you start simple with trace.

### application performance monitoring (APM) tools that fit

Commercial and open-source APM tools (Datadog, New Relic, Sentry Performance, Grafana Cloud) collect latency, error rates, and distributed traces from production. The modern vendor-neutral approach is to instrument once with **OpenTelemetry** and export to whichever backend you use — this avoids rewriting instrumentation when switching vendors.

### What part of the code should I profile?
Now let's delve into profiling specifics. The term "profiling" is mainly used for performance testing, and the purpose of performance testing is to find bottlenecks by doing deep analysis. So you can use tracing tools to help you with profiling. Recall that tracing is when software developers log information about a software execution. Therefore, logging performance metrics is also a way to perform profiling analysis.

But we're not restricted to tracing. As profiling gains mindshare in the mainstream, we now have tools that perform profiling directly. Now the question is, what parts of the software do we profile (measure its performance metrics)?

### Typically, we profile:

- Method or function (most common)
- Lines (similar to method profiling, but doing it line by line)
- Memory (memory usage)

### What metrics should I profile?

- Speed (time)
- Calls (frequency)
- Method and line profiling

Both cProfile and profile are modules available in the Python 3 language. The numbers produced by these modules can be formatted into reports via the pstats module.

Here's an example of cProfile showing the numbers for a script:
```python
import cProfile
import re

cProfile.run('re.compile("foo|bar")')

197 function calls (192 primitive calls) in 0.002 seconds
```

### Memory profiling
Another common component to profile is the memory usage. The purpose is to find memory leaks and optimize the memory usage in your Python programs. The modern toolkit:

- **`tracemalloc`** (stdlib, 3.4+) — snapshots of Python allocations with tracebacks to the allocating line; zero dependencies, safe to use in production diagnostics.
- **memray** (Bloomberg) — the current gold standard: tracks native (C-extension) allocations too, produces flamegraphs, and can attach to a running process.
- `objgraph` — still handy for answering "what is keeping this object alive" via reference graphs.

```python
import tracemalloc

tracemalloc.start()
run_workload()
snapshot = tracemalloc.take_snapshot()
for stat in snapshot.statistics("lineno")[:10]:
    print(stat)               # top-10 allocation sites with sizes
```

**Why `tracemalloc`/memray over older tools (`pympler`):** they attribute memory to the exact source line (not just to a class), cover C-extension allocations (memray), and are actively maintained.

### Deterministic profiling versus statistical profiling
When we do profiling, it means we need to monitor the execution. That in itself may affect the underlying software being monitored. Either we monitor all the function calls and exception events, or we use random sampling and deduce the numbers. The former is known as deterministic profiling, and the latter is statistical profiling. Of course, each method has its pros and cons. Deterministic profiling can be highly precise, but its extra overhead may affect its accuracy. Statistical profiling has less overhead in comparison, with the drawback being lower precision.

cProfile, which I covered earlier, uses deterministic profiling. Let's look at another open source Python profiler that uses statistical profiling: pyinstrument.

### `pyinstrument`
Pyinstrument differentiates itself from other typical profilers in two ways. First, it emphasizes that it uses statistical profiling instead of deterministic profiling. It argues that while deterministic profiling can give you more precision than statistical profiling, the extra precision requires more overhead. The extra overhead may affect the accuracy and lead to optimizing the wrong part of the program. Specifically, it states that using deterministic profiling means that "code that makes a lot of Python function calls invokes the profiler a lot, making it slower." This is how results get distorted and the wrong part of the program gets optimized.

### `py-spy` and `scalene`

Two statistical profilers every senior should know in 2026:

- **py-spy** — attaches to a **running process by PID** with no code changes and negligible overhead (`py-spy top --pid 1234`, `py-spy record -o profile.svg --pid 1234`). It is the standard answer to "production is slow *right now*, what is it doing?" — something cProfile cannot do because it requires restarting the program under the profiler.
- **scalene** — profiles CPU, memory and GPU together, and separates time spent in Python from time spent in native code, so you immediately see whether the fix is "vectorise this loop" or "the bottleneck is inside numpy already".

## `resource` module	

This module provides basic mechanisms for measuring and controlling system resources utilized by a program.

Symbolic constants are used to specify particular system resources and to request usage information about either the current process or its children.

`resource.getrusage(who)`
This function returns an object that describes the resources consumed by either the current process or its children, as specified by the who parameter. The who parameter should be specified using one of the RUSAGE_* constants described below.

A simple example:
```python
from resource import *
import time

# a non CPU-bound task
time.sleep(3)
print(getrusage(RUSAGE_SELF))

# a CPU-bound task
for i in range(10 ** 8):
   _ = 1 + 1
print(getrusage(RUSAGE_SELF))
```

## context managers contextlib decorator, with-enabled class

The with statement in Python is a quite useful tool for properly managing external resources in your programs. It allows you to take advantage of existing context managers to automatically handle the setup and teardown phases whenever you're dealing with external resources or with operations that require those phases.

Besides, the context management protocol allows you to create your own context managers so you can customize the way you deal with system resources. So, what's the with statement good for?

```python
# writable.py

class WritableFile:
    def __init__(self, file_path):
        self.file_path = file_path

    def __enter__(self):
        self.file_obj = open(self.file_path, mode="w")
        return self.file_obj

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file_obj:
            self.file_obj.close()
```

```python
>>> from contextlib import contextmanager

>>> @contextmanager
... def writable_file(file_path):
...     file = open(file_path, mode="w")
...     try:
...         yield file
...     finally:
...         file.close()
...

>>> with writable_file("hello.txt") as file:
...     file.write("Hello, World!")
```

```python
# site_checker_v1.py
import aiohttp
import asyncio

async def check(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            print(f"{url}: status -> {response.status}")
            html = await response.text()
            print(f"{url}: type -> {html[:17].strip()}")

async def main():
    await asyncio.gather(
        check("https://realpython.com"),
        check("https://pycoders.com"),
    )

asyncio.run(main())
```

## `contextlib` Beyond `@contextmanager`

### Key Features:
- `ExitStack` / `AsyncExitStack` — compose a *dynamic* number of context managers.
- `suppress`, `closing`, `nullcontext`, `redirect_stdout`, `chdir` (3.11+).
- `@asynccontextmanager` and `aclosing` (3.10+) for async resources.
- `ContextDecorator` — one object usable as both `with` block and decorator.

### `ExitStack`: when the number of resources is not known statically

```python
from contextlib import ExitStack

def merge(paths: list[str], out: str) -> None:
    with ExitStack() as stack:
        files = [stack.enter_context(open(p)) for p in paths]
        target = stack.enter_context(open(out, "w"))
        stack.callback(print, "done")          # arbitrary cleanup, LIFO order
        for f in files:
            target.writelines(f)
```

**Why `ExitStack` rather than nesting `with`:** a nested `with` requires you to know the count at compile time. The naive alternative — a `try/finally` closing a list of handles — leaks every already-opened file if `open()` raises halfway through the list. `ExitStack` unwinds in LIFO order and, crucially, guarantees that *everything entered so far* is exited even if a later `enter_context` blows up.

```python
stack = ExitStack()
conn = stack.enter_context(connect())
closer = stack.pop_all().close      # hand ownership to the caller
```

**Why `pop_all()` matters:** it is the standard idiom for a factory that opens several resources and must either return them all successfully or clean up everything on partial failure — the Python answer to RAII-style transactional acquisition.

### Async composition

```python
from contextlib import AsyncExitStack, asynccontextmanager, aclosing

@asynccontextmanager
async def session(url: str):
    conn = await connect(url)
    try:
        yield conn
    finally:
        await conn.close()          # runs even if the body raises or is cancelled

async def main(urls: list[str]) -> None:
    async with AsyncExitStack() as stack:
        conns = [await stack.enter_async_context(session(u)) for u in urls]
        ...

async def consume(agen):
    async with aclosing(agen) as it:      # 3.10+
        async for item in it:
            if item is None:
                break                      # early exit still runs the generator's finally
```

**Why `aclosing` is not optional:** breaking out of an `async for` leaves the async generator suspended, and its cleanup runs only when the loop's shutdown hooks eventually finalise it — non-deterministically, possibly after the event loop is closed. `aclosing` calls `aclose()` immediately, making resource release deterministic. The same applies to sync generators via `contextlib.closing`.

### Small but high-value helpers

```python
from contextlib import nullcontext, chdir, suppress

cm = open(path) if path else nullcontext(sys.stdout)   # one code path, not two
with cm as fh:
    fh.write("data")

with chdir("/tmp"):        # 3.11+, restores the previous cwd (NOT thread-safe: cwd is per-process)
    ...
```

**Why `nullcontext`:** it removes the duplicated `with`-block/no-`with`-block branches that otherwise appear whenever a resource is optional, keeping a single tested code path.

# Unit testing in Python	
## Mock objects

A mock object substitutes and imitates a real object within a testing environment. It is a versatile and powerful tool for improving the quality of your tests.

One reason to use Python mock objects is to control your code's behavior during testing.

For example, if your code makes HTTP requests to external services, then your tests execute predictably only so far as the services are behaving as you expected. Sometimes, a temporary change in the behavior of these external services can cause intermittent failures within your test suite.

```python
>>> from unittest.mock import Mock
>>> mock = Mock()
>>> mock
<Mock id='4561344720'>
```

A Mock must simulate any object that it replaces. To achieve such flexibility, it creates its attributes when you access them.

```python
>>> from unittest.mock import Mock

>>> # Create a mock object
... json = Mock()

>>> json.loads('{"key": "value"}')
<Mock name='mock.loads()' id='4550144184'>

>>> # You know that you called loads() so you can
>>> # make assertions to test that expectation
... json.loads.assert_called()
>>> json.loads.assert_called_once()
>>> json.loads.assert_called_with('{"key": "value"}')
>>> json.loads.assert_called_once_with('{"key": "value"}')
```

```python
datetime = Mock()
datetime.datetime.today.return_value = "tuesday"
requests = Mock()
requests.get.side_effect = Timeout
```

```python
@patch('my_calendar.requests')
    def test_get_holidays_timeout(self, mock_requests):
            mock_requests.get.side_effect = Timeout
```
or
```python
with patch('my_calendar.requests') as mock_requests:
            mock_requests.get.side_effect = Timeout
```

And there are MagicMock and Async Mock as well.

## Coverage

Coverage.py is one of the most popular code coverage tools for Python. It uses code analysis tools and tracing hooks provided in Python standard library to measure coverage. Current versions support CPython 3.9+ and PyPy3. You can use Coverage.py with both unittest and pytest.

## Testing Frameworks: pytest, unittest, doctests

**Note:** The original `nose` project is no longer maintained (last release 2015). `nose2` exists but is also not actively developed. **`pytest` is now the de facto standard** for Python testing.

### pytest (Recommended)
```python
# test_example.py
def test_addition():
    assert 1 + 1 == 2

def test_string():
    assert "hello".upper() == "HELLO"
```

```bash
pytest test_example.py -v
```

**Key pytest features:**
- Simple `assert` statements (no special assertion methods needed)
- Powerful fixtures for setup/teardown
- Parametrized tests
- Rich plugin ecosystem
- Better output and debugging

### unittest (Standard Library)
Built into Python, follows xUnit pattern:
```python
import unittest

class TestExample(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(1 + 1, 2)
```

The doctest module searches for pieces of text that look like interactive Python sessions, and then executes those sessions to verify that they work exactly as shown. There are several common ways to use doctest:

- To check that a module's docstrings are up-to-date by verifying that all interactive examples still work as documented.

- To perform regression testing by verifying that interactive examples from a test file or a test object work as expected.

- To write tutorial documentation for a package, liberally illustrated with input-output examples. Depending on whether the examples or the expository text are emphasized, this has the flavor of "literate testing" or "executable documentation".

`python example.py -v`

## pytest in depth: fixtures, parametrize, monkeypatch

`assert`-based tests are the smallest part of what pytest gives you. The parts that matter at senior level are dependency injection via fixtures, and test data generation.

### Fixtures: setup/teardown as dependency injection

```python
# conftest.py - fixtures here are visible to every test in the directory tree
import pytest
from myapp.db import Session, create_engine

@pytest.fixture(scope="session")
def engine():
    eng = create_engine("postgresql+psycopg://localhost/test")
    yield eng                     # everything after yield is teardown
    eng.dispose()

@pytest.fixture
def session(engine):              # fixtures depend on other fixtures
    with engine.connect() as conn:
        tx = conn.begin()
        yield Session(bind=conn)
        tx.rollback()             # every test gets a clean DB, cheaply

@pytest.fixture
def user(session):
    return session.add(User(email="a@b.c"))
```

```python
def test_user_can_login(user, session):   # just name what you need
    assert login(user.email, "pw") is not None
```

**Why fixtures over `unittest.setUp()`:** `setUp` runs for *every* test in the class whether it is needed or not, and sharing setup between classes requires inheritance. Fixtures are requested by name, composed like a dependency graph, cached per scope (`function`/`class`/`module`/`session`), and their teardown is guaranteed even on failure. Expensive resources get `scope="session"`; per-test isolation is done with a transaction rollback rather than by rebuilding the world.

### Parametrize instead of loops

```python
@pytest.mark.parametrize(
    ("raw", "expected"),
    [
        ("1h", 3600),
        ("90m", 5400),
        pytest.param("", 0, marks=pytest.mark.xfail(reason="issue #412")),
    ],
)
def test_parse_duration(raw, expected):
    assert parse_duration(raw) == expected
```

**Why not a `for` loop inside one test:** a loop stops at the first failure and reports one test. Parametrize produces N independent test IDs, so the report tells you *exactly which inputs* broke and you can rerun one with `pytest -k "90m"`.

### Built-in fixtures worth knowing

```python
def test_writes_report(tmp_path):             # real temp dir, auto-cleaned
    write_report(tmp_path / "r.csv")
    assert (tmp_path / "r.csv").exists()

def test_reads_config(monkeypatch):           # auto-undone after the test
    monkeypatch.setenv("API_URL", "http://x")
    monkeypatch.setattr("myapp.clock.now", lambda: FIXED_TIME)

def test_logs_failure(caplog):
    with caplog.at_level("ERROR"):
        do_thing()
    assert "payment declined" in caplog.text
```

**Why `monkeypatch` over `unittest.mock.patch` for env vars and attributes:** it is undone automatically at teardown even if the test raises, and it reads as one line instead of a decorator stack. Use `mock.patch`/`MagicMock` when you need call assertions; use `monkeypatch` for state.

**Patch where it is *used*, not where it is defined.** `from x import get` binds a new name, so `patch("x.get")` has no effect on the caller — patch `mymodule.get`.

### Async tests

```python
# pyproject.toml
[tool.pytest.ini_options]
asyncio_mode = "auto"          # plain `async def test_...` works, no decorator needed

@pytest.fixture
async def client():
    async with AsyncClient(transport=ASGITransport(app), base_url="http://t") as c:
        yield c

async def test_health(client):
    assert (await client.get("/health")).status_code == 200
```

`pytest-asyncio` (or `anyio`'s plugin, if you support trio too) supplies the event loop. Testing an ASGI app through `ASGITransport` exercises the real routing/middleware stack **without opening a socket**, so tests stay fast and port-conflict-free.

### Beyond unit tests

- **hypothesis** — property-based testing: state the invariant, let it search for the counterexample and shrink it. Finds the edge cases your example-based tests never thought of.
- **testcontainers** — spin up a real PostgreSQL/Redis in Docker for integration tests. A fake that behaves differently from the real DB is worse than no test.
- **time-machine** / **freezegun** — freeze the clock instead of sleeping.
- **respx** / **responses** — stub HTTP at the transport layer, not by mocking your own code.
- **pytest-xdist** (`-n auto`) — parallelism; it also *proves* your tests are independent.

### Configuration that prevents rot

```toml
[tool.pytest.ini_options]
addopts = "--strict-markers --strict-config -ra"
filterwarnings = ["error"]     # a DeprecationWarning today is a broken build next year
testpaths = ["tests"]
```

**On coverage:** treat it as a *detector of untested areas*, not a target. Enforce a floor (`--cov-fail-under=80`) so it cannot fall, but remember 100% line coverage says nothing about whether the assertions are meaningful — use `--cov-branch` and review the tests themselves.

# Memory management in Python

## 3 generations of GC

The main garbage collection algorithm used by CPython is reference counting. The basic idea is that CPython counts how many different places there are that have a reference to an object. Such a place could be another object, or a global (or static) C variable, or a local variable in some C function. When an object's reference count becomes zero, the object is deallocated. If it contains references to other objects, their reference counts are decremented. Those other objects may be deallocated in turn, if this decrement makes their reference count become zero, and so on. The reference count field can be examined using the sys.getrefcount function (notice that the value returned by this function is always 1 more as the function also has a reference to the object when called):
```python
x = object()
sys.getrefcount(x)
2
y = x
sys.getrefcount(x)
3
del y
sys.getrefcount(x)
2
```

**Note (Python 3.12+):** PEP 683 introduced **immortal objects** — `None`, `True`, `False`, small integers, and interned strings now have a fixed huge sentinel refcount that never changes, so `sys.getrefcount(None)` no longer returns a meaningful number. Under the free-threaded build, refcounts are biased/deferred, so the exact values in examples like the above are not reproducible there either.

The main problem with the reference counting scheme is that it does not handle reference cycles. For instance, consider this code:
```python
container = []
container.append(container)
sys.getrefcount(container)
3
del container
```

In this example, container holds a reference to itself, so even when we remove our reference to it (the variable "container") the reference count never falls to 0 because it still has its own internal reference. Therefore it would never be cleaned just by simple reference counting. For this reason some additional machinery is needed to clean these reference cycles between objects once they become unreachable. This is the cyclic garbage collector, usually called just Garbage Collector (GC), even though reference counting is also a form of garbage collection.

In order to limit the time each garbage collection takes, the GC uses a popular optimization: generations. The main idea behind this concept is the assumption that most objects have a very short lifespan and can thus be collected shortly after their creation. This has proven to be very close to the reality of many Python programs as many temporary objects are created and destroyed very fast. The older an object is the less likely it is that it will become unreachable.

To take advantage of this fact, all container objects are segregated into three spaces/generations. Every new object starts in the first generation (generation 0). The previous algorithm is executed only over the objects of a particular generation and if an object survives a collection of its generation it will be moved to the next one (generation 1), where it will be surveyed for collection less often. If the same object survives another GC round in this new generation (generation 1) it will be moved to the last generation (generation 2) where it will be surveyed the least often.

Generations are collected when the number of objects that they contain reaches some predefined threshold, which is unique for each generation and is lower the older the generations are. These thresholds can be examined using the gc.get_threshold function:

### module gc

```python
import gc
gc.get_threshold()
(700, 10, 10)
```
```python
>>> import gc
>>> gc.get_count()
(596, 2, 1)
```

You can trigger a manual garbage collection process by using the `gc.collect()` method

```python
import gc
class MyObj:
    pass


# Move everything to the last generation so it's easier to inspect
# the younger generations.

gc.collect()
0

# Create a reference cycle.

x = MyObj()
x.self = x

# Initially the object is in the youngest generation.

gc.get_objects(generation=0)
[..., <__main__.MyObj object at 0x7fbcc12a3400>, ...]

# After a collection of the youngest generation the object
# moves to the next generation.

gc.collect(generation=0)
0
gc.get_objects(generation=0)
[]
gc.get_objects(generation=1)
[..., <__main__.MyObj object at 0x7fbcc12a3400>, ...]
```
The garbage collector module provides the Python function is_tracked(obj), which returns the current tracking status of the object.

### Which type of objects are tracked?
 For this reason some additional machinery is needed to clean these reference cycles between objects once they become unreachable. This is the cyclic garbage collector, usually called just Garbage Collector (GC), even though reference counting is also a form of garbage collection.

As a general rule, instances of atomic types aren't tracked and instances of non-atomic types (containers, user-defined objects…) are. However, some type-specific optimizations can be present in order to suppress the garbage collector footprint of simple instances. Some examples of native types that benefit from delayed tracking:

Tuples containing only immutable objects (integers, strings etc, and recursively, tuples of immutable objects) do not need to be tracked

Dictionaries containing only immutable objects also do not need to be tracked

## recommendations for GC usage	

General rule: Don't change garbage collector behavior

## Memory leaks/deleters issues

The Python program, just like other programming languages, experiences memory leaks. Memory leaks in Python happen if the garbage collector doesn't clean and eliminate the unreferenced or unused data from Python.

Python developers have tried to address memory leaks through the addition of features that free unused memory automatically.

However, some unreferenced objects may pass through the garbage collector unharmed, resulting in memory leaks.

# Threading and multiprocessing in Python	
## GIL (Definition, algorithms in 2.x and 3.x)

The mechanism used by the CPython interpreter to assure that only one thread executes Python bytecode at a time. This simplifies the CPython implementation by making the object model (including critical built-in types such as dict) implicitly safe against concurrent access. Locking the entire interpreter makes it easier for the interpreter to be multi-threaded, at the expense of much of the parallelism afforded by multi-processor machines.

However, some extension modules, either standard or third-party, are designed so as to release the GIL when doing computationally-intensive tasks such as compression or hashing. Also, the GIL is always released when doing I/O.

Past efforts to create a "free-threaded" interpreter (one which locks shared data at a much finer granularity) were not successful for a long time because performance suffered in the common single-threaded case. **This has finally changed:** Python 3.13 shipped an experimental free-threaded build (PEP 703), and since Python 3.14 the free-threaded build is officially supported (PEP 779), with single-threaded overhead reduced to roughly 5-10%. The default build still uses the GIL, but CPython is now on a path where the GIL is optional.

```python
>>> import sys
>>> # Python 2.x used sys.getcheckinterval() (removed in Python 3.2)
>>> # Python 3.2+ uses time-based switching instead of instruction-based:
>>> sys.getswitchinterval()
0.005  # 5 milliseconds - the interval between thread switches
>>> sys.setswitchinterval(0.01)  # Can be adjusted if needed
```

**Note:** `sys.getcheckinterval()` and `sys.setcheckinterval()` were removed in Python 3.2. The old approach checked every N instructions; the new approach uses a time-based interval (default 5ms) which is more fair and predictable.

The problem in this mechanism was that most of the time the CPU-bound thread would reacquire the GIL itself before other threads could acquire it. This was researched by David Beazley and visualizations can be found here.

This problem was fixed in Python 3.2 (released in 2011; the new GIL was implemented in 2009) by Antoine Pitrou who added a mechanism of looking at the number of GIL acquisition requests by other threads that got dropped and not allowing the current thread to reacquire GIL before other threads got a chance to run.


## Threads(modules thread, threading; class Queue; locks)
Straight forward:
```python
from time import sleep, perf_counter
from threading import Thread

def task():
    print('Starting a task...')
    sleep(1)
    print('done')

start_time = perf_counter()

# create two new threads
t1 = Thread(target=task)
t2 = Thread(target=task)

# start the threads
t1.start()
t2.start()

# wait for the threads to complete
t1.join()
t2.join()

end_time = perf_counter()

print(f'It took {end_time- start_time: 0.2f} second(s) to complete.')
```

Better:

```python
from concurrent.futures import ThreadPoolExecutor
from time import sleep

def cube(x):
    result = x * x * x
    print(f'Cube of {x}: {result}')
    return result

if __name__ == '__main__':
    values = [3, 4, 5, 6]
    
    with ThreadPoolExecutor(max_workers=5) as executor:
        # map applies cube to every value, preserving input order
        results = list(executor.map(cube, values))
    
    print("\nResults:")
    for value, result in zip(values, results):
        print(f"Cube of {value}: {result}")


```

Operations associated with `queue.Queue` are: 

- `maxsize` – Number of items allowed in the queue.
- `empty()` – Return True if the queue is empty, False otherwise.
- `full()` – Return True if there are maxsize items in the queue. If the queue was initialized with maxsize=0 (the default), then full() never returns True.
- `get()` – Remove and return an item from the queue. If queue is empty, wait until an item is available.
- `get_nowait()` – Return an item if one is immediately available, else raise `queue.Empty` (`asyncio.Queue` raises `QueueEmpty`).
- `put(item)` – Put an item into the queue. If the queue is full, wait until a free slot is available before adding the item.
- `put_nowait(item)` – Put an item into the queue without blocking. If no free slot is immediately available, raise `queue.Full` (`asyncio.Queue` raises `QueueFull`).
- `qsize()` – Return the number of items in the queue.

## Processes(multiprocessing, Process, Queue, Pipe, Value, Array, Pool, Manager)	

Simple case:

```python
#!/usr/bin/python

from multiprocessing import Process
import time

def fun():

    print('starting fun')
    time.sleep(2)
    print('finishing fun')

def main():

    p = Process(target=fun)
    p.start()
    p.join()


if __name__ == '__main__':

    print('starting main')
    main()
    print('finishing main')
```

Nice pool:

```python
#!/usr/bin/python

import time
from timeit import default_timer as timer
from multiprocessing import Pool, cpu_count

def square(n):
    time.sleep(2)
    return n * n

def main():
    start = timer()
    print(f'starting computations on {cpu_count()} cores')
    values = (2, 4, 6, 8)

    with Pool() as pool:
        res = pool.map(square, values)
        print(res)

    end = timer()
    print(f'elapsed time: {end - start}')

if __name__ == '__main__':
    main()
```

**Note:** the old `pipes` module (shell-pipeline helper) was deprecated by PEP 594 and **removed in Python 3.13** — use `subprocess` instead. It was unrelated to `multiprocessing.Pipe()`, which is a two-way IPC channel between processes and remains fully supported.

## Choosing a concurrency model: a decision guide

Knowing *how* threads, processes, asyncio and subinterpreters work is table stakes. The senior question is *which one to reach for*, and being able to justify it.

| Model | Best for | Parallel CPU? | Cost per unit | Data sharing | Main risk |
|---|---|---|---|---|---|
| `asyncio` | Many concurrent I/O ops (HTTP, sockets, DB) | No | ~KB, thousands OK | Same memory, single thread | One blocking call stalls everything |
| `threading` / `ThreadPoolExecutor` | Blocking I/O, libs that release the GIL (numpy, zlib, DB drivers) | Partly | ~8MB stack | Same memory + locks | Race conditions, deadlocks |
| `multiprocessing` / `ProcessPoolExecutor` | Pure-Python CPU-bound work | Yes | ~30-50MB + startup | Pickle / shared memory | Serialization cost, harder debugging |
| Subinterpreters (`concurrent.interpreters`, 3.14+) | CPU-bound with lighter isolation than processes | Yes | Lighter than a process | Explicit channels/queues | Young ecosystem, C extensions may not support it |
| Free-threaded build (3.14+, official) | CPU-bound shared-state work in threads | Yes | Thread-cheap | Same memory + locks | Needs FT-compatible wheels; ~5-10% single-thread overhead |
| External queue (Celery, arq, Dramatiq) | Work that outlives a request | Yes (many hosts) | A whole worker | Broker | Operational complexity |

### The decision path

1. **Is the work I/O-bound?** → `asyncio` if the whole stack is async-capable, otherwise threads. Adding processes to an I/O-bound workload buys nothing but memory usage.
2. **Is it CPU-bound in pure Python?** → processes today. Consider the free-threaded build or subinterpreters if all your dependencies have wheels for it.
3. **Is it CPU-bound inside C/Rust (numpy, polars, pillow, cryptography)?** → **threads are fine**, because those libraries release the GIL. Reaching for processes here is a common over-engineering.
4. **Does the caller need the result now?** If not, it belongs in a task queue, not in the web process.

### The rule that breaks async services

Never call blocking code from a coroutine. One `requests.get()` or `time.sleep()` inside the event loop stops *every* concurrent request on that worker, which looks like a mysterious latency spike under load rather than an obvious error.

```python
import asyncio

# WRONG - blocks the entire event loop
def handler():
    data = requests.get(url).json()          # blocking library

# RIGHT - use an async client
async def handler():
    async with httpx.AsyncClient() as c:
        data = (await c.get(url)).json()

# RIGHT - unavoidable blocking work goes to a thread
async def handler():
    return await asyncio.to_thread(legacy_blocking_call, arg)
```

**Always bound your concurrency.** `asyncio.Semaphore(20)` around outbound calls prevents your own service from DoS-ing a downstream one. "Unbounded fan-out" is the single most common async production incident.

## How to avoid GIL restrictions (C extensions)

Only C threads:
```c
#include "Python.h"
...
PyObject *pyfunc(PyObject *self, PyObject *args)
{
    ...
    Py_BEGIN_ALLOW_THREADS
      
    // Threaded C code. 
    // Must not use Python API functions
    ...
    Py_END_ALLOW_THREADS
    ...
    return result;
}
```
Mixing C and Python:

**Note:** `PyEval_InitThreads()` is deprecated since Python 3.9 and removed in Python 3.13. Since Python 3.7, the GIL is always initialized, so explicit initialization is no longer needed. For modern Python (3.9+), simply use the GIL macros directly:

```c
#include <Python.h>
...
// No need for PyEval_InitThreads() in Python 3.9+
// Just use Py_BEGIN_ALLOW_THREADS / Py_END_ALLOW_THREADS as needed
```


# Distributing and documentation in Python	

## Modern packaging: `pyproject.toml`, PEP 517/518/621

**`distutils` was removed in Python 3.12** (deprecated in 3.10, see PEP 632). `setup.py` is no longer a required file, and running `python setup.py install` has been deprecated since 2021 — it invokes the build system as a script instead of through the standardised interface.

Three PEPs define modern packaging:

- **PEP 518** — `[build-system]`: declare *what builds your package*, in an isolated environment. Before it, `setup.py` had to import `setuptools` that might not be installed yet — a bootstrap paradox that broke CI constantly.
- **PEP 517** — a build *backend* interface, so `pip`/`build`/`uv` can build any project without knowing anything about setuptools. This is what made Rust and C++ backends possible.
- **PEP 621** — `[project]`: static, declarative metadata. Tools can read your name, version and dependencies **without executing arbitrary Python**, which is both faster and safer.

### A complete modern package

```toml
# pyproject.toml - the only required config file
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "mypackage"
version = "1.2.0"                    # or use dynamic versioning
description = "Does one thing well"
readme = "README.md"
requires-python = ">=3.12"
license = "MIT"                      # PEP 639 SPDX expression
authors = [{ name = "Jane Dev", email = "jane@example.com" }]
dependencies = ["httpx>=0.28"]
classifiers = ["Programming Language :: Python :: 3.14"]

[project.urls]
Source = "https://github.com/me/mypackage"

[project.scripts]
mycli = "mypackage.cli:main"         # generates a console entry point on install
```

```
mypackage/
├── pyproject.toml
├── README.md
├── LICENSE
├── src/
│   └── mypackage/
│       ├── __init__.py
│       └── core.py
└── tests/
```

**Why the `src/` layout:** without it, `import mypackage` in your tests picks up the *source directory* on `sys.path`, not the installed package. Missing files in your wheel then pass CI and fail for users. With `src/`, tests can only import what was actually installed.

### Choosing a build backend

| Backend | Use when |
|---|---|
| **hatchling** | Pure-Python default; fast, zero boilerplate, good VCS versioning |
| **setuptools** | Legacy projects, complex `MANIFEST.in`, existing C extensions |
| **flit-core** | Tiny single-module libraries |
| **maturin** | The package is a Rust (PyO3) extension |
| **scikit-build-core** | C/C++ with CMake |
| **uv_build** | uv-native projects wanting the fastest build path |

### Building and publishing

```bash
uv build            # or: python -m build  -> dist/*.whl and dist/*.tar.gz
uv publish          # or: twine upload dist/*
```

Always ship **both** artifacts: the **wheel** (`.whl`) installs without a build step, and the **sdist** (`.tar.gz`) lets distributions and exotic platforms rebuild from source.

**Publish from CI with Trusted Publishing, not an API token.** PyPI supports OIDC: your GitHub Actions workflow exchanges a short-lived identity token for an upload token, so there is no long-lived secret in the repo to leak.

```yaml
# .github/workflows/release.yml
permissions:
  id-token: write            # required for OIDC - no PYPI_TOKEN secret needed
jobs:
  publish:
    environment: pypi
    steps:
      - uses: actions/checkout@v5
      - run: pipx run build
      - uses: pypa/gh-action-pypi-publish@release/v1
```

Publish to **TestPyPI** first; a version number on PyPI can be yanked but **never reused**. For compiled packages, build wheels for every platform with **cibuildwheel**, and prefer the **stable ABI** (`abi3`) so one wheel covers many Python versions instead of one wheel each.

## Documentation autogeneration: sphinx, pydoc, etc.

`autosummary`, an extension for the Sphinx documentation tool.

`autodoc`, a Sphinx-based processor that processes/allows reST doc strings.

`pdoc`, a simple Python 3 command line tool and library to auto-generate API documentation for Python modules. Supports Numpydoc / Google-style docstrings, doctests, reST directives, PEP 484 type annotations, custom templates ...

`MkDocs` + `mkdocstrings` — the most common modern choice for project documentation: Markdown-based, renders API docs from docstrings and type annotations, with the popular Material theme. (Note: the `pdoc3` fork is stale — prefer plain `pdoc` or mkdocstrings.)

`PyDoc`, a documentation browser (in HTML) and/or an off-line reference manual. Also in the standard library as pydoc.

`pydoctor`, a replacement for now inactive Epydoc, born for the needs of Twisted project.

`Doxygen` can create documentation in various formats (HTML, LaTeX, PDF, ...) and you can include formulas in your documentation (great for technical/mathematical software). Together with Graphviz, it can create diagrams of your code (inhertance diagram, call graph, ...). Another benefit is that it handles not only Python, but also several other programming languages like C, C++, Java, etc.

# Python and C interaction

## C ext API,call C from python, call python from C	

Simple C function:
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    FILE *fp = fopen("write.txt", "w");
    fputs("Real Python!", fp);
    fclose(fp);
    return 1;
}
```
And make it python-compatible:

```c
#include <Python.h>

static PyObject *method_fputs(PyObject *self, PyObject *args) {
    char *str, *filename = NULL;
    int bytes_copied = -1;

    /* Parse arguments */
    if(!PyArg_ParseTuple(args, "ss", &str, &filename)) {
        return NULL;
    }

    FILE *fp = fopen(filename, "w");
    bytes_copied = fputs(str, fp);
    fclose(fp);

    return PyLong_FromLong(bytes_copied);
}

static PyMethodDef FputsMethods[] = {
    {"fputs", method_fputs, METH_VARARGS, "Python interface for fputs C library function"},
    {NULL, NULL, 0, NULL}
};


static struct PyModuleDef fputsmodule = {
    PyModuleDef_HEAD_INIT,
    "fputs",
    "Python interface for the fputs C library function",
    -1,
    FputsMethods
};
```

Build it with `setuptools` (note: `distutils` was removed in Python 3.12):

**Modern approach using pyproject.toml:**
```toml
# pyproject.toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "fputs"
version = "1.0.0"
description = "Python interface for the fputs C library function"

[tool.setuptools]
ext-modules = [
    {name = "fputs", sources = ["fputsmodule.c"]}
]
```

**Legacy approach using setup.py:**
```python
from setuptools import setup, Extension

setup(
    name="fputs",
    version="1.0.0",
    description="Python interface for the fputs C library function",
    ext_modules=[Extension("fputs", ["fputsmodule.c"])]
)
```

```bash
# Modern build command
pip install build
python -m build
pip install dist/*.whl
```

```python
>>> import fputs
>>> fputs.__doc__
'Python interface for the fputs C library function'
>>> fputs.__name__
'fputs'
>>> # Write to an empty file named `write.txt`
>>> fputs.fputs("Real Python!", "write.txt")
13
>>> with open("write.txt", "r") as f:
>>>     print(f.read())
'Real Python!'
```

https://realpython.com/build-python-c-extension-module/

## cffi, swig, SIP, boost-python

`cffi` - C Foreign Function Interface for Python. Interact with almost any C code from Python, based on C-like declarations that you can often copy-paste from header files or documentation. https://cffi.readthedocs.io/en/latest/

```python
from cffi import FFI
ffibuilder = FFI()

# cdef() expects a single string declaring the C types, functions and
# globals needed to use the shared object. It must be in valid C syntax.
ffibuilder.cdef("""
    float pi_approx(int n);
""")

# set_source() gives the name of the python extension module to
# produce, and some C source code as a string.  This C code needs
# to make the declarated functions, types and globals available,
# so it is often just the "#include".
ffibuilder.set_source("_pi_cffi",
"""
     #include "pi.h"   // the C header of the library
""",
     libraries=['piapprox'])   # library name, for the linker

if __name__ == "__main__":
    ffibuilder.compile(verbose=True)
```

`SWIG` is an interface compiler that connects programs written in C and C++ with scripting languages such as Perl, Python, Ruby, and Tcl http://www.swig.org/exec.html

`SIP` is a collection of tools that makes it very easy to create Python bindings for C and C++ libraries. https://www.riverbankcomputing.com/static/Docs/sip/examples.html

### Boost

https://www.boost.org/doc/libs/1_78_0/libs/python/doc/html/tutorial/index.html

Following C/C++ tradition, let's start with the "hello, world". A C++ Function:

```char const* greet()
{
   return "hello, world";
}
```
can be exposed to Python by writing a Boost.Python wrapper:

```
#include <boost/python.hpp>

BOOST_PYTHON_MODULE(hello_ext)
{
    using namespace boost::python;
    def("greet", greet);
}
```

That's it. We're done. We can now build this as a shared library. The resulting DLL is now visible to Python. Here's a sample Python session:

```python
>>> import hello_ext
>>> print(hello_ext.greet())
hello, world
```

# Python tools

## Python standard library	

https://docs.python.org/3/library/

Just read their names and short descriptions at least. You would be surprised how many task you can do with pure python.

## Advanced knowledge of standard library: 
- `math` This module provides access to the mathematical functions defined by the C standard. https://docs.python.org/3/library/math.html
- `random` This module implements pseudo-random number generators for various distributions. https://docs.python.org/3/library/random.html
- `re`  This module provides regular expression matching operations similar to those found in Perl. https://docs.python.org/3/library/re.html
- `sys` This module provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter. It is always available. https://docs.python.org/3/library/sys.html
- `os` This module provides a portable way of using operating system dependent functionality. If you just want to read or write a file see open(), if you want to manipulate paths, see the os.path module, and if you want to read all the lines in all the files on the command line see the fileinput module. For creating temporary files and directories see the tempfile module, and for high-level file and directory handling see the shutil module. https://docs.python.org/3/library/os.html
- `time`, 
- `datetime`, 
- `argparse` Parser for command-line options, arguments and sub-commands https://docs.python.org/3/library/argparse.html
- `optparse` Soft-deprecated: no longer slated for removal (the docs relaxed the deprecation in 3.13), but not developed further — use `argparse` for new code.

