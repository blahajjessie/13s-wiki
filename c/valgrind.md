---
title: "Using Valgrind"
layout: default
has_children: false
parent: "C Concepts"
nav_order: 1

---

By Anthony Umemoto

# What is Valgrind?

Valgrind is diagnostics tool that watches how your program is using memory. Getting comfortable using valgrind will be a useful skill when debugging those dreaded memory leaks.

To install valgrind, use the command:
```
$ sudo apt install valgrind
```

To use valgrind, use the command:
```
$ valgrind ./<executable>
```

For example:
```
$ valgrind ./sorter -l 100
```
You just have to put `valgrind` in front of the command you'd normally use to run your program!

# Example Usage

The messages valgrind outputs can be pretty cryptic at times, so in this example you'll see some of the most common ones. You can follow along, as this will be a step-by-step tutorial.

## Initial Code

