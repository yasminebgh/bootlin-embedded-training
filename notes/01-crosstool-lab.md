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

1. ./bootstrap: Ct-ng uses the Autotools build system (autoconf, automake, autoheader, libtool) to generate portable and cofigurable build scripts, while we are working directly from a Git repo, the configure script and related build files are not included, so we need ./bootstrap scripts tp generate those files (configure scipt, aclocal.m4, makefile.inconfig.h.in, autoheader...) => so need build scripts first by running ./bootstrap which runs autotools commands 

2. ./configure --enable-local: Tells crosstool-ng to not install yourself in my computer's main folders, instead just stay here in this folder so I can run you directly, without the 
--enable-local, it would copy stuff in places like /usr/local/bin, that leads to the need of using sudo and also to overwritting pther versions
The ./configure is to get ready to build, checks for compilers, libraries and tools needed, creates makefiles, instructions for make to actually build the program 
(Prepare the kitchen before cooking, checking and preparing all the ingredients and setting the table before starting)

3. make: Do the cooking, reads the makefile, compiles the code into an actual program, and runs the necessary steps in the right order until the program is built

4. ./ct-ng <command>: The main executable program of crosstool-ng, to configure, build and manage the cross-compilation toolchain
Crosstool-ng comes with a set of ready-made configuration files for various typical setups: Crosstool-ng calls
them samples.
5. ./ct-ng sample: in this case the aarch64-unknown-linux-uclibc -> sets the .config file with all the settings needed to build a toolchain for the aarch64 architecture using the 
uclibc C library

6. ./ct-ng menuconfig: To refine the configuration, to customize the toolchain without editing config files by hand(change of linux version(It’s important that the kernel headers
used in the toolchain are not more recent than the kernel that will run on the board)  gcc version, C library and compiler...) 

7. ./ct-ng build: Produce the toolchain => Downloads all necessary sources (GCC, binutils, C library, the ernel headers...), Configures and compiles each component and creates the final toolchain and install it in the specified folder ![build process](screenshots/Toolchain_buildin)


When compiling, the cross-compiler uses the sysroot to find the correct headers and files for the target system ( a mini "fake" of the target's device file system inside your PC)
