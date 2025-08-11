# Lab <1> – <Building a toolchain>

Building a cross-compiling toolchain -> Learn how to compile your own crosstool toolchain for musl C library 

#Goal: 
The goals of this lab are to be able to configure the crosstool-ng tool and to execute crosstool-ng and build my own toolchain

cross-compiler: A set up of tools chained together to produce a binary code to be executed on a host machine different from the machine it runs on.

Components: 
-> Binutils (comes with a linker) Binary utilities to generate and manipulate binaries for a given CPU architecture
-> C library: to perform basic tasks (memory allocations, printing output on a terminal, managing file access...), needs to know the API to the kernel to decide what features are present or needed ( the API is provided by the kernel headers)
-> Kernel hearders: 

STEPS:

1. GMP
2. MPFR
3. mpc
4. binutils: 
5. core pass 1 compiler: Bootstrap: minimal compiler that doesnt need header or start file, to bootstrap the process
6. Kernel headers: Basic systems interface that tell your programs how to talk to the system
7. C libraries and start files: Basic parts of the C standard library that programs need to start running (startup code.., C runtime)
8. Core pass 2 compiler: A more complete compiler that uses Kernel and C libraries headers/start files to compile more complex code
9. Complete C library: The full standard library providing all functions and utilities for programs
10. Final compiler: The fully featured compiler built using core pass 2 and C complete library

## Commands Used  
