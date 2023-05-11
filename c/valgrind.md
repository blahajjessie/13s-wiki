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

# Valgrind's Output

You'll see a lot of different messages from valgrind, since it's a very robust tool. The end goal is always the same though:

```
$ valgrind ./example
==4763== Memcheck, a memory error detector
==4763== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==4763== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==4763== Command: ./example
==4763== 
I just used malloc() to make my array!
Filling it up with...
0 1 2 3 4 
And now I use free()
==4763== 
==4763== HEAP SUMMARY:
==4763==     in use at exit: 0 bytes in 0 blocks
==4763==   total heap usage: 2 allocs, 2 frees, 1,044 bytes allocated
==4763== 
==4763== All heap blocks were freed -- no leaks are possible
==4763== 
==4763== For lists of detected and suppressed errors, rerun with: -s
==4763== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

You'll want to see just your program's output in the middle (which you can differentiate by the lack of `==####==`). 

In `HEAP SUMMARY`, there should be an equal number of `allocs` and `frees`. 

You should see the message `All heap blocks were freed -- no leaks are possible`. 

And, at the bottom it should say `0 errors from 0 contexts (suppressed: 0 from 0)`.

If the output looks like this, then you know your program successfully passes valgrind.

# DWARF 4

Valgrind looks directly at the executable, and doesn't actually know what your C code looks like. Because of this, figuring out what valgrind is telling can be pretty tricky.

To make its messages a little easier to read, we can use the `-gdward-4` compiler flag when compiling. This will format the executable using DWARF 4, which you can read more about [here](https://dwarfstd.org/dwarf4std.html).

Here's a comparison of valgrind's output with, and without DWARF 4:

### dwarf.c:
```
1  #include <stdlib.h>
2  
3  int main(void) {
4      int *alloc1 = (int *) malloc(sizeof(int) * 10);
5      int *alloc2 = (int *) malloc(sizeof(int) * 10);
6 
7      free(alloc1);
8      return 0;
9  }
```
This program will cause a memory leak since `alloc2` is never free'd.

### Compiled with: `clang dwarf.c -o dwarf`
```
$ valgrind --leak-check=full ./dwarf
==2586== Memcheck, a memory error detector
==2586== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==2586== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==2586== Command: ./dwarf
==2586== 
==2586== 
==2586== HEAP SUMMARY:
==2586==     in use at exit: 40 bytes in 1 blocks
==2586==   total heap usage: 2 allocs, 1 frees, 80 bytes allocated
==2586== 
==2586== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2586==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==2586==    by 0x401166: main (in /home/user/dwarf)
==2586== 
==2586== LEAK SUMMARY:
==2586==    definitely lost: 40 bytes in 1 blocks
==2586==    indirectly lost: 0 bytes in 0 blocks
==2586==      possibly lost: 0 bytes in 0 blocks
==2586==    still reachable: 0 bytes in 0 blocks
==2586==         suppressed: 0 bytes in 0 blocks
==2586== 
==2586== For lists of detected and suppressed errors, rerun with: -s
==2586== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

Here, valgrind is run with `--leak-check=full` which is useful for figuring out where blocks of memory were lost.

The useful information is:
```
==2586== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2586==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==2586==    by 0x401166: main (in /home/user/dwarf)
```
This tells us that the leak is from a block allocated with `malloc()` in `main()`. But which `malloc()`? If your program is large, with lots of memory allocations and frees happening, pinning down which `malloc()` this is referring to can be difficult.

### Compiled with: `clang -gdwarf-4 dwarf.c -o dwarf`
```
$ valgrind --leak-check=full ./dwarf
==2742== Memcheck, a memory error detector
==2742== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==2742== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==2742== Command: ./dwarf
==2742== 
==2742== 
==2742== HEAP SUMMARY:
==2742==     in use at exit: 40 bytes in 1 blocks
==2742==   total heap usage: 2 allocs, 1 frees, 80 bytes allocated
==2742== 
==2742== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2742==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==2742==    by 0x401166: main (dwarf.c:5)
==2742== 
==2742== LEAK SUMMARY:
==2742==    definitely lost: 40 bytes in 1 blocks
==2742==    indirectly lost: 0 bytes in 0 blocks
==2742==      possibly lost: 0 bytes in 0 blocks
==2742==    still reachable: 0 bytes in 0 blocks
==2742==         suppressed: 0 bytes in 0 blocks
==2742== 
==2742== For lists of detected and suppressed errors, rerun with: -s
==2742== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

Looking at the same section:
```
==2742== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2742==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==2742==    by 0x401166: main (dwarf.c:5)
```
Next to `main` it now says that the leak is from the `malloc()` on line 5 in dwarf.c, which is the `malloc()` for the `alloc2` array.