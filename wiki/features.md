---
layout: wiki
title: Features of exceptions4c
tags: [ "Featured" ]
---

# Features of `exceptions4c`

This library has got `1000` distinctive features:

  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/exception**handling.png> `000`: **<#Exception**Handling Exception Handling>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/polymorphism.png> `001`: **<#Polymorphism Polymorphism>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/chained**exceptions.png> `010`: **<#Chained**Exceptions Chained Exceptions>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/dispose**pattern.png> `011`: **<#Dispose**Pattern Dispose Pattern>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/signal**handling.png> `100`: **<#Signal**Handling Signal Handling>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/multi-thread.png> `101`: **<#Multi-Thread Multi-Thread>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/thoroughly**tested.png> `110`: **<#Thoroughly**Tested Thoroughly Tested>**
  - <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/24x24/fully**documented.png> `111`: **<#Fully**Documented Fully Documented>**

You may also be interested in the `1000` <reasons> to use the library.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/exception**handling.png> Exception Handling

ANSI C does not provide direct support for error handling. By convention, the programmer is expected to test every possible error code returned from functions. To make things worse, there is also an external variable called `errno` which needs to be checked. This **traditional** C way of detecting errors is cumbersome and error prone. In addition, error handling code is usually intrusive and clutters everything up.

On the other hand, exception handling is a mechanism to handle the occurrence of special conditions that change the normal flow of program execution. When an exceptional situation is found, the program throws an exception and the execution is transferred to the part of the program responsible for handling such error condition. Many modern programming languages supports exception handling. And **`exceptions4c` brings the power of exceptions to C programs**.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/polymorphism.png> Polymorphism

Error conditions can often be organized hierarchically. At the root of this hierarchy are generic errors. Other error conditions are specific cases of their predecessors. For example, a hypothetical `Stack` object could cause errors of the generic type `StackException`; this error condition could have two specific cases: `StackOverflowException` and `StackUnderflowException`.

`exceptions4c` allows you to handle both specific and generic error conditions. Every exception type has a `parent` exception type. The "child" type is a more specific case of the "parent" type. Thus, **the exception types form a **hierarchy**** that will be useful. When defining `catch` blocks, you need to specify which type of exceptions this block is capable of handling. If you specify a generic type, then the block is implicitly capable of handling any of the specific types.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/chained**exceptions.png> Chained Exceptions

Exceptions can be attached to a `cause`: another exception that caused this exception to get thrown. This is also known as the **chained exception facility**, as the cause can, itself, have a cause, and so on, leading to a **chain** of exceptions, each caused by another.

As a developer, you don't need to worry about **initializing** the `cause` of an exception. When you `throw` an exception inside a `catch` or `finally` block, your exception's `cause` is automatically set to the current exception.

When you are dealing with an exception, you can inspect its `cause` and handle it just like any other exception.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/dispose**pattern.png> Dispose Pattern

The dispose pattern is a design pattern which is used to handle resource cleanup. `exceptions4c` implements this pattern and ensures that a resource will be disposed, no matter what exception is thrown while the resource was being used.

On the one hand, you define a code block to acquire the resource, and specify a function that will dispose it once it is no longer needed. On the other hand, you define the block of code that will be actually making use of the resource. **The library will dispose the resource, even if an exception is thrown**. In addition, the function responsible for disposing the resource will know whether the block of code using the resource succeeded or failed and and can act accordingly (for example, by commiting or rolling back a database transaction).

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/signal**handling.png> Signal Handling

A signal is a software interrupt delivered to a process. The operating system uses signals to report exceptional situations to an executing program. Most of the signals will, by default, halt the program as soon as they are raised. For example, if a program attempted to perform an integer division by zero, the operating system would send a signal SIGFPE and then the program would crash.

When you look at it, signals are really very similar exceptions. But handling signals in ANSI C is a thorny problem. `exceptions4c` tries to make things easier for the programmer: in addition to **exception** handling, `exceptions4c` features **signal** handling. **The libary will trap any signal sent to your program and will convert it to a convenient exception**; then it can be **caught** just like a regular exception.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/multi-thread.png> Multi-Thread

You can enable the multi-thread version of the library by defining `E4C**THREADSAFE` at compiler level. This version is **completely **reentrant** and, therefore, thread-safe**. It relies on `pthreads`, the **POSIX** application programming interface for writing multithreaded applications. This API is available for most operating systems and platforms.

The usage of the framework does not vary between single and multithreaded programs. The same semantics apply. The only caveat is that the behavior of signal handling is undefined in a multithreaded program, so use this feature with caution.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/thoroughly**tested.png> Thoroughly Tested

A testing framework has been developed to ensure the library's reliability. There is a convenience `Makefile` inside the `test` directory. It will download (through `wget`) any missing files and then compile them altogether. You are encouraged to try it yourself and make sure that everything works as expected. When the tests are done, a report is generated in HTML. It comes in handy if any of the tests failed: you can click a link and file a bug very easily.

There are many test suites, containing **more than 50 unit tests**. There are also tests designed to check platforms requirements. For example, the operating system and compiler have to support signal handling, otherwise the library won't be able to map signals to exceptions. Some of the platforms the library has been tested on, fail to handle some of the signals.

----

# <https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/icons/40x40/fully**documented.png> Fully Documented

This wiki tries to describe in detail all the characteristics of the library. Although the API is simple and self-explanatory, examples and tutorials are provided for ease of use. A fair amount of effort is invested in mantaining all this information up to date.

Besides from the wiki, `exceptions4c` is fully documented, starting with the very source code. It takes a disciplined approach but, as a result, the API documentation can be **automatically generated with <http://www.doxygen.org/ Doxygen>**. It lists all functions, macros, variables and structures you need to know for using `exceptions4c`.

----

<https://raw.githubusercontent.com/guillermocalvo/exceptions4c/master/etc/img/logo/exceptions4c**128.png>