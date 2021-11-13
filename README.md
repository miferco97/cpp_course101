# C++ 101 course index <!-- omit in toc --> 
**TABLE OF CONTENTS**

- [1. Compiling and linking](#1-compiling-and-linking)
  - [1.1 GNU C++ building](#11-gnu-c-building)
  - [1.2 CMake compilation](#12-cmake-compilation)
- [2. Before beggining](#2-before-beggining)
  - [2.1 Header files](#21-header-files)
  - [2.2 Project Files Organization](#22-project-files-organization)
  - [2.3 Precompiler directives](#23-precompiler-directives)
    - [2.3.1 ```#include```](#231-include)
    - [2.3.1 ```#define```](#231-define)
    - [2.3.3 ```#pragma```](#233-pragma)
    - [2.3.4 Conditionals](#234-conditionals)
- [3. Basic Concepts](#3-basic-concepts)
  - [3.1 Variables](#31-variables)
    - [3.1.1 Basic Types](#311-basic-types)
    - [3.1.2 Value assigments](#312-value-assigments)
  - [3.2 Conditions, branches and loops](#32-conditions-branches-and-loops)
  - [3.3 Control Flow](#33-control-flow)
  - [3.4 Functions](#34-functions)
  - [3.5 Function overloading](#35-function-overloading)
  - [3.6 Namespaces](#36-namespaces)
- [4. Memory managent](#4-memory-managent)
  - [4.1 Life-time and Scope](#41-life-time-and-scope)
  - [4.2 Pointers and References (arrow operator)](#42-pointers-and-references-arrow-operator)
  - [4.3 Pass by value and by reference](#43-pass-by-value-and-by-reference)
  - [4.4 Arrays](#44-arrays)
    - [4.4.1 String Literals](#441-string-literals)
  - [4.5 Memory allocation](#45-memory-allocation)
  - [4.6 Stack vs Heap Memory](#46-stack-vs-heap-memory)
- [5. Object Oriented Programming](#5-object-oriented-programming)
  - [5.1 Class](#51-class)
    - [5.1.1 Member Attributes](#511-member-attributes)
    - [5.1.2 Member Functions](#512-member-functions)
    - [5.1.3 This in a class](#513-this-in-a-class)
    - [5.1.4 Class vs Object](#514-class-vs-object)
  - [5.2 Struct vs Class](#52-struct-vs-class)
  - [5.3 Constructors and Destructor](#53-constructors-and-destructor)
    - [5.3.1 Member Initializer List](#531-member-initializer-list)
  - [5.4 Inheritance](#54-inheritance)
  - [5.5 Virtual Function](#55-virtual-function)
    - [5.5.1 Pure Virtual Functions (Interfaces)](#551-pure-virtual-functions-interfaces)
  - [5.6 Visibility in classes](#56-visibility-in-classes)
  - [5.7 Operator overloading](#57-operator-overloading)
- [6. Advanced Type use](#6-advanced-type-use)
  - [6.1 Auto](#61-auto)
  - [6.2 Const](#62-const)
  - [6.3 Enums](#63-enums)
  - [6.4 Static](#64-static)
    - [6.4.1 File scope](#641-file-scope)
    - [6.4.2 Function scope](#642-function-scope)
    - [6.4.3 Class scope](#643-class-scope)
  - [6.5 Templates](#65-templates)
  - [6.6 Smart Pointers](#66-smart-pointers)
    - [6.6.1 Unique ptr](#661-unique-ptr)
    - [6.6.2 Shared ptr](#662-shared-ptr)
  - [6.7 Mutable](#67-mutable)
  - [6.8 Casting](#68-casting)
    - [6.8.1 Static Casting](#681-static-casting)
    - [6.8.2 Dynamic Casting](#682-dynamic-casting)
- [7. Advanced Functions](#7-advanced-functions)
  - [7.1 Function pointers](#71-function-pointers)
  - [7.2 Lambda functions](#72-lambda-functions)
  - [7.3 Optional data in function](#73-optional-data-in-function)
  - [7.4 Threads and concurrency](#74-threads-and-concurrency)
  - [7.5 Friend Functions](#75-friend-functions)
- [8. Advanced concepts](#8-advanced-concepts)
  - [8.1 Implicit and Explicit Conversion](#81-implicit-and-explicit-conversion)
  - [8.1 Iterators](#81-iterators)
  - [8.2 L-values && R-values](#82-l-values--r-values)
  - [8.3 Copy Operator](#83-copy-operator)
  - [8.4 Move Semantics](#84-move-semantics)
  - [8.5 Return Value Optimization (RVO)](#85-return-value-optimization-rvo)
- [9. STD Library Basics](#9-std-library-basics)
  - [9.1 STD Input Output Stream ```<iostream>```](#91-std-input-output-stream-iostream)
    - [9.1.1 std::cout](#911-stdcout)
  - [9.2 STD containers](#92-std-containers)
    - [9.2.1 std::array](#921-stdarray)
    - [9.2.2 std::vector](#922-stdvector)
    - [9.2.3 std::string](#923-stdstring)
    - [9.2.4 std::pair, std::tuple](#924-stdpair-stdtuple)
    - [9.2.5 std::unorderer_container](#925-stdunorderer_container)


# 1. Compiling and linking
C++ is a programming language that needs to compile the code into machine code generated before running an executable. This compiled code is dependant of the microprocessor (concretely the microprocessor instructions set, like x86) and the Operative System used. This means that executables generated in Windows won't work in a MacOS or Linux, or code generated for a Desktop computer won't run on a Raspberry Pi. 

The compiling process in C++ is a three steps process [1]:
  1. **Pre-procesing:** In this step the pre-processor directives are processed. This directives which are identified in code by the prefix #,define behaviours that are to be carried out on the source code before its compiled.
  2. **Compilation:** Compiling is the next step in the process and is concerned with turning the source code that we write into something that a computer can understand, machine code. It’s at the compilation stage that we will be warned about any errors in our code that cause our code to not compile.
  3. **Linking:** The final stage of the process is linking which is concerned with taking our output from the previous step and linking it all together to produce the actual executable or library. Assuming no errors occur during this stage, an executable file or library is generated.

This three steps are commonly grouped into a process called **build**.

There are diferent compilers and tools for compiling C++ programs. We will only talk about two ways of compiling: compiling "*manually*" using a compiler (like GNU c++ or clang) directly, and automating this build process using CMake.

## 1.1 GNU C++ building

GNU C++ is a compilation controller part of the GNU Compiler Collection (GCC).
The compiler invocation command is ```g++ ```, which is used for preprocessing, compilation, assembly and linking of source code to generate an executable file. The different “flags” of g++ command allow us to stop this process at the intermediate stage. 

When building a c++ program a .cpp file with a ```main()``` function must be provided to the compiler, with all the other .cpp files required for the execution of this ```main()``` function. Header files (.hpp) are included using preprocessing directives (using sentences like ```#include <lib>``` in the .cpp files). Moreover, when a external library is wanted to be used where to find this library must be provided to the compiler. (A library is just a reusable collection of functions, classes and objects that share a common purpose, for example, a math library.)

A basic main.cpp building example can be:
~~~
$g++ main.cpp -o main 
~~~
It compiles a file ```main.cpp``` ***located in the same folder*** where the ```g++``` comand is invoked. If the compilation is successfull it will generate an executable called ```main.o```.

If more files were required it would be like: 
~~~
$g++ main.cpp file1.cpp file2.cpp file3.cpp ... -o main 
~~~

This building command can be modified using g++ compilation flags, some of the most usefull are:
  - ```-o <filename>``` : Compiles and links files into an executable named ```<filename>```. The default filename is ```a.out```.
  - ```-Wall``` : Show all warnings. It turns on all standard C++ warnings about code that might cause unexpected or undefined behavior.
  - ```-pedantic``` : Issues all warnings demanded by strict ISO C++ rules if you want to be extra safe.
  - ```--std=c++<##>``` : Uses version ```<##>``` of C++ when compiling. This will allow you to use specific features of that C++ version. Typically, we have you use ```--std=c++17```.
  - ```-I/<absolute-path>``` : Adds ```<absolute-path>``` to the compiler’s search paths. The path must written from the root of the filesystem, ```/```.
  - ```-L/<absolute-path>``` : Adds ```<absolute-path>``` to the compiler’s search paths for **binary libraries**. The path must written from the root of the filesystem, ```/```.
  - ```-l<library-name>``` : Links with the library compiled (.a or .so files) named ```<library-name>``` .
  - ```-c``` : Compiles and assembles files but doesn’t link them. This is useful when building large projects to separate file compilation and minimize what is re-compiled.

## 1.2 CMake compilation

<!-- TODO: complete this -->

# 2. Before beggining

> For this course we will be using C++17 standard, if you use a different c++ version some implementations may differ.

## 2.1 Header files 
<!-- TODO: complete this -->
This is because when a library is generated, the header files are the files that shows all the functions and classes that the library provides and how to use them. The .cpp files of a library used to be already compiled for reducing compilation time.

## 2.2 Project Files Organization
In order to organize a c++ code project different approaches can be used, however most of them have a rule in common, header files must be separated from the .cpp code. 
> project_name/ <br>
>  - include/
>    - obj1.hpp
>    - ...
>  - src/<br>
>    - main.cpp
>    - obj1.cpp 
>    - ..

## 2.3 Precompiler directives
### 2.3.1 ```#include``` 
### 2.3.1 ```#define```
### 2.3.3 ```#pragma```
### 2.3.4 Conditionals 


# 3. Basic Concepts
## 3.1 Variables
### 3.1.1 Basic Types
### 3.1.2 Value assigments
## 3.2 Conditions, branches and loops
## 3.3 Control Flow
## 3.4 Functions
## 3.5 Function overloading
## 3.6 Namespaces

# 4. Memory managent
## 4.1 Life-time and Scope
## 4.2 Pointers and References (arrow operator)
## 4.3 Pass by value and by reference
## 4.4 Arrays
### 4.4.1 String Literals
## 4.5 Memory allocation 
<!-- The new keyword-->
## 4.6 Stack vs Heap Memory

# 5. Object Oriented Programming
## 5.1 Class
### 5.1.1 Member Attributes
### 5.1.2 Member Functions
### 5.1.3 This in a class
### 5.1.4 Class vs Object
## 5.2 Struct vs Class
## 5.3 Constructors and Destructor
### 5.3.1 Member Initializer List
## 5.4 Inheritance
## 5.5 Virtual Function
### 5.5.1 Pure Virtual Functions (Interfaces)
## 5.6 Visibility in classes
## 5.7 Operator overloading

# 6. Advanced Type use
## 6.1 Auto
## 6.2 Const
## 6.3 Enums
## 6.4 Static
### 6.4.1 File scope
### 6.4.2 Function scope
### 6.4.3 Class scope
## 6.5 Templates
## 6.6 Smart Pointers
### 6.6.1 Unique ptr
### 6.6.2 Shared ptr
## 6.7 Mutable
## 6.8 Casting
### 6.8.1 Static Casting
### 6.8.2 Dynamic Casting


# 7. Advanced Functions
## 7.1 Function pointers
## 7.2 Lambda functions
## 7.3 Optional data in function
## 7.4 Threads and concurrency
## 7.5 Friend Functions

# 8. Advanced concepts
## 8.1 Implicit and Explicit Conversion
## 8.1 Iterators
## 8.2 L-values && R-values
## 8.3 Copy Operator
## 8.4 Move Semantics
## 8.5 Return Value Optimization (RVO)

# 9. STD Library Basics 
## 9.1 STD Input Output Stream ```<iostream>```
### 9.1.1 std::cout

## 9.2 STD containers
### 9.2.1 std::array
### 9.2.2 std::vector
### 9.2.3 std::string
### 9.2.4 std::pair, std::tuple
### 9.2.5 std::unorderer_container


--<br>
References:<br>
[1] https://gamedevunboxed.com/learn-how-to-compile-a-c-program/ <br>
[2] https://bytes.usc.edu/cs104/wiki/gcc/ <br>
[3] https://www.geeksforgeeks.org/compiling-with-g-plus-plus/ <br>
[4] 0