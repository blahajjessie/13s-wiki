---
title: "Options and Arguments"
layout: default
has_children: false
parent: "C Concepts"
has_toc: true
nav_order: 1

---

# Options and Arguments

argc, argv, getopt, optarg, oh my

by Ben Grant

{: .no_toc}

## Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

## argc and argv

You may know that the `main` function in C has parameters: `argc` and `argv`. These store your program's _command-line arguments_ (like the `-a` in `ls -a`), and you can use them directly or use the `getopt` standard library function to parse them more easily.

`argc` has type `int`, and it simply stores the number of arguments your program was passed. This is needed since as you may know, you can't determine the length of an array in C given only a pointer. `argv` has type `char **` (i.e. an array of `char *`s, or an array of strings), and it stores the actual arguments.

With this knowledge, we can write a simple program that just prints out all the arguments it was given:

```c
#include <stdio.h>

int main(int argc, char **argv) {
    printf("argc = %d\n", argc);
    for (int i = 0; i < argc; i += 1) {
        printf("argv[%d] = %s\n", i, argv[i]);
    }
    return 0;
}
```

Let's compile it and then run it with varying arguments:

```
$ clang args.c -o args
$ ./args
argc = 1
argv[0] = ./args
$ ./args foo bar baz
argc = 4
argv[0] = ./args
argv[1] = foo
argv[2] = bar
argv[3] = baz
$ ./args "hello world" foo\ bar
argc = 3
argv[0] = ./args
argv[1] = hello world
argv[2] = foo bar
```

Here are some lessons we can learn:

1. `argv[0]` contains the name of the program as it was executed, in this case `./args`. Later we'll see that if we rename the executable, `argv[0]` changes accordingly.
2. The rest of the arguments (from `argv[1]` to `argv[argc - 1]`) are null-terminated strings containing whichever arguments we specified on the command line.
3. You have probably realized by now that arguments are separated by spaces. This separation is done by your shell, before the program you run sees the arguments. If you want to write an argument with actual space characters in it, you need to use quotes or escape the space as we saw in the last example.

What happens if we name our program something else?

```
$ mv args args2
$ ./args2
argc = 1
argv[0] = ./args2
$ mkdir -p some_directory
$ cd some_directory
$ ../args2
argc = 1
argv[0] = ../args2
```

Nice, `argv[0]` always matches. Many programs use `argv[0]` in help and error messages, so that the program name it prints out is consistent with how the user is running it. For instance:

```c
printf("usage: %s [-ace] <file1> [file2...]\n", argv[0]);
```

```c
printf("%s: error: invalid argument\n", argv[0]);
```

```
usage: ../args2 [-ace] <file1> [file2...]
../args2: error: invalid argument
```

That usage message is formatted similarly to how many other command-line programs do it. It means:

- The program may take any combination of the flags `-a`, `-c`, or `-e`, but they are all optional.
- After the arguments, you must specify at least one filename, and you may specify more filenames if you want.

Usually there would be text following that explains what each flag does.

## getopt

It's possible to accept arguments just by parsing `argv` directly. However, it's inconvenient to do this. The C standard library includes the function `getopt` which makes argument parsing a lot easier.

`getopt` takes three arguments: `argc` and `argv`, and then an _options string_ which defines which options are acceptable. This string just has one character for each option you want to allow. Options followed by a colon require an argument afterwards (like `-i input_file` as opposed to `-S`).

Here's the basic template for how you will be using getopt:

```c
#include <stdio.h>
// for getopt:
#include <unistd.h>

#define OPTIONS "abc:"

int main(int argc, char **argv) {
    int opt;
    while ((opt = getopt(argc, argv, OPTIONS)) != -1) {
        switch (opt) {
        case 'a':
            printf("-a passed\n");
            break;
        case 'b':
            printf("-b passed\n");
            break;
        case 'c':
            printf("-c passed with argument %s\n", optarg);
            break;
        default:
            fprintf(stderr, "invalid arguments\n");
            return 1;
        }
    }
    return 0;
}
```

`getopt` usually returns the option passed as a single character. If there are no more options it returns `-1`, so we use that to end our loop. If there's an error (an invalid option or an option missing an argument), it returns the character `'?'`. We handle that in our `default:` case, since that isn't an argument we want to handle. Inside that part, we just print out an error message and exit with a nonzero value to indicate an error. In your actual programs you might want to also print a help message in that situation.

```
$ clang getopt.c -o getopt
$ ./getopt
$ ./getopt -b
-b passed
$ ./getopt -a -b
-a passed
-b passed
$ ./getopt -ba
-b passed
-a passed
$ ./getopt -c
./getopt: option requires an argument -- 'c'
unknown argument
$ ./getopt -c hello
-c passed with argument hello
$ ./getopt -d
./getopt: invalid option -- 'd'
unknown argument
```

Here are some more things we can observe from those examples:

1. `getopt` process options in the order they were given.
2. `getopt` has no concept of an option that is required. You have to implement that yourself. For instance, if you require an output file be specified with `-o`, you could do something like:

    ```c
    char *outfile = NULL;
    while ((opt = getopt(argc, argv, OPTIONS)) != -1) {
        switch (opt) {
        // ...
        case 'o':
            outfile = optarg;
            break;
        // ...
        }
    }

    if (outfile == NULL) {
        fprintf(stderr, "%s: error: an output file must be specified\n", argv[0]);
        return 1;
    }
    ```

    Also, even though the value of `optarg` changes as `getopt` processes different command-line arguments, it is okay to save `optarg` in a local variable as we have done above. This is because `optarg` points somewhere within the `argv` array, so when we save its value, our local variable will always point to the same position even if `optarg` changes (`getopt` doesn't modify `argv`).

3. You can stick together many arguments in a row and `getopt` will give you them separately (`-ba` is the same as `-b -a`).
4. `optarg` is always a string. If you want an argument that is a number, you have to convert it to a number yourself (probably using `strtoull`), and potentially output an error if the string could not be parsed.
5. `getopt` prints its own error messages for invalid options and missing arguments: the lines

    ```
    ./getopt: option requires an argument -- 'c'
    ./getopt: invalid option -- 'd'
    ```

    did not come from any code we wrote. We do still need to exit the program (otherwise, `getopt` keeps processing more options) or print more useful help if we want to.
