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

The messages valgrind outputs can be pretty cryptic at times, so in these examples you'll see some of the most common ones.

<br/>

## Definitely Lost Memory

<b>Initial Code: array.c</b>
```
#include <stdlib.h>
#include <stdio.h>

int *int_array(int length) {
    return (int *) malloc(sizeof(int) * length);
}

int main(void) {
    int *array = int_array(10);

    for (int i = 0; i < 10; i++) {
        array[i] = i + 1;
        printf("%d ", array[i]);
    }
    printf("\n");

    return 0;
}
```

This program allocates an array, fills in its elements, and prints them out. When this program is run on its own, the output works as expected:

```
$ ./array
1 2 3 4 5 6 7 8 9 10 
```

However, if valgrind is run with it:
```
$ valgrind ./array 
==2604== Memcheck, a memory error detector
==2604== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==2604== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==2604== Command: ./array
==2604== 
1 2 3 4 5 6 7 8 9 10 
==2604== 
==2604== HEAP SUMMARY:
==2604==     in use at exit: 40 bytes in 1 blocks
==2604==   total heap usage: 2 allocs, 1 frees, 1,064 bytes allocated
==2604== 
==2604== LEAK SUMMARY:
==2604==    definitely lost: 40 bytes in 1 blocks
==2604==    indirectly lost: 0 bytes in 0 blocks
==2604==      possibly lost: 0 bytes in 0 blocks
==2604==    still reachable: 0 bytes in 0 blocks
==2604==         suppressed: 0 bytes in 0 blocks
==2604== Rerun with --leak-check=full to see details of leaked memory
==2604== 
==2604== For lists of detected and suppressed errors, rerun with: -s
==2604== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

We can see that 40 bytes were "definitely lost". This is because the array was never freed with:
```
free(array);
```

Often, it won't be entirely clear what hasn't been freed yet. Following the suggestion valgrind gives under the leak summary, rerunning with `$ valgrind --leak-check=full ./array` will give us some additional information:
```
==2721== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==2721==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==2721==    by 0x40115A: int_array (in /home/user/array)
==2721==    by 0x401188: main (in /home/user/array)
```

The important stuff are the function names it shows. This will tell us which `malloc()` in our code originally allocated the block of memory that was lost. With that information, we can check to make sure that those specific allocations are also freed properly, instead of checking everywhere we allocate memory.

In our case, we just have to add one line:

<b>Fixed Code: array.c</b>
```
#include <stdlib.h>
#include <stdio.h>

int *int_array(int length) {
    return (int *) malloc(sizeof(int) * length);
}

int main(void) {
    int *array = int_array(10);

    for (int i = 0; i < 10; i++) {
        array[i] = i + 1;
        printf("%d ", array[i]);
    }
    printf("\n");

    free(array); // ADDED A FREE
    return 0;
}
```

<br/>

## Invalid Write

<b>Initial Code: char.c</b>
```
#include <stdio.h>

int main(void) {
    char *ptr = NULL;
    *ptr = 'a';
    printf("%c", *ptr);

    return 0;
}
```

If this gets compiled an run, it will result in a segmentation fault:
```
$ ./char
Segmentation fault (core dumped)
```
This is not a very descriptive message, and debugging one is often a long process. Valgrind can give us some more information on what exactly caused it:

<b>Valgrind Output:</b>
``` 
$ valgrind ./char
==2995== Memcheck, a memory error detector
==2995== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==2995== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==2995== Command: ./char
==2995== 
==2995== Invalid write of size 1
==2995==    at 0x40114B: main (in /home/user/char)
==2995==  Address 0x0 is not stack'd, malloc'd or (recently) free'd
==2995== 
==2995== 
==2995== Process terminating with default action of signal 11 (SIGSEGV)
==2995==  Access not within mapped region at address 0x0
==2995==    at 0x40114B: main (in /home/user/char)
==2995==  If you believe this happened as a result of a stack
==2995==  overflow in your program's main thread (unlikely but
==2995==  possible), you can try to increase the size of the
==2995==  main thread stack using the --main-stacksize= flag.
==2995==  The main thread stack size used in this run was 8388608.
==2995== 
==2995== HEAP SUMMARY:
==2995==     in use at exit: 0 bytes in 0 blocks
==2995==   total heap usage: 0 allocs, 0 frees, 0 bytes allocated
==2995== 
==2995== All heap blocks were freed -- no leaks are possible
==2995== 
==2995== For lists of detected and suppressed errors, rerun with: -s
==2995== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
Segmentation fault (core dumped)
```

Again, valgrind gives a very descriptive message that can be daunting decipher. The important information here is:
```
==2995== Invalid write of size 1
==2995==    at 0x40114B: main (in /home/user/char)
==2995==  Address 0x0 is not stack'd, malloc'd or (recently) free'd
```

This is telling us that the program tried to "write" to a memory address it was not allowed to. The address it was trying to access was `0x0`, which is `NULL`.

Since the `ptr` variable is `NULL`, yet is trying to be dereferenced:
```
char *ptr = NULL;
*ptr = 'a';
```

To fix this, we can either create a variable for `ptr` to reference:

```
char letter;
char *ptr = &letter;
*ptr = 'a';
```

 or allocate memory for `ptr` to reference:

```
char *ptr = (char *) malloc(sizeof(char));
*ptr = 'a';
```