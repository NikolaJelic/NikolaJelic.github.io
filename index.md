# Getting started

This is a short introduction for setting up a working C++ development environment.

After going through all these steps, you should be able to create, compile, debug and run a C++ program.

## Required tools

	- IDE/Text Editor
	- Compiler
	- CMake and Ninja
	- Debugger 

## IDE/Text Editor

This is where you write all of your code. There are multiple different IDEs(Integrated Development Environments) and Text Editors.

For this article we will use a very popular text editor - **Visual Studio Code** which can be found [here.](https://code.visualstudio.com/download)

Another good option would be the IDE with a similar name **Visual Studio** found [here.](https://visualstudio.microsoft.com/downloads/)

It should be noted that Visual studio isn't available for Linux, so Visual Studio Code is still recommended.



### 	Visual Studio Code plugins 


​	One of the biggest benefits of VSCode are its extensibility and versatility which are a result of its plugin system.

​	Some recommended  plugins are:

   - [C/C++(Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
   - [Clang-Format](https://marketplace.visualstudio.com/items?itemName=xaver.clang-format)
   - [Clang-tidy](https://marketplace.visualstudio.com/items?itemName=notskm.clang-tidy)
   - [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
   - [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)


## Compiler

   Most likely you are writing code to accomplish or make something, but just written code alone doesn't do much. 

   If you want to actually execute the program you have written, you need to first compile it and for that you need a *compiler*

   There are several different C++ compilers like:

   - [clang](https://clang.llvm.org/)
   - [gcc/g++](https://gcc.gnu.org/)
   - [mingw](http://mingw-w64.org/doku.php)
   - and others

   We will be using *clang* together with [*cmake*](https://cmake.org/download/)

### 	Installation

#### 		Linux

   - Install [**CMake**](https://cmake.org/download/)

   - Install clang using your favorite packet manager or follow the instructions [**here**](https://clang.llvm.org/get_started.html)
   - You can also insallit from a pre-built binary found [**here**](https://releases.llvm.org/download.html)

#### 		Windows

   - Install [**CMake**](https://cmake.org/download/)
   - Clang can be found [**here**](https://llvm.org/builds/)
   - After installing Clang, you should also add it to $PATH. (like [*this*](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/))
   - If you are using Visual Studio, there is no need to manualy insall a compiler since you will be able to do that during the installation of Visual Studio  


## CMake and Ninja

- CMake is an open-source, cross-platform family of tools designed to build, test and package software. 
- CMake is used to control the software compilation process using simple platform and compiler independent configuration files, and generate native makefiles and workspaces that can be used in the compiler environment of your choice. 
- In short: CMake does stuff so you don't have to
	### Installation 
You can download it [**here**](https://cmake.org/download/) or use your favorite packet manager if you are running Linux

## Authoring an Executable

### Project Workspace

Create a new directory for the project, somewhere, say `hello`

- This is the **project root** (`./`)
- The **author** of the project (you) must ensure to keep it agnostic of anything before/above `./` (where `hello` is located)
- This ensures that a **user** of the project (also you) can clone/download and build it anywhere they like
- Similarly, ideally the project should not require any environment variables etc to have been set up prior

### Project Files

Create a new source file: `main.cpp`, and write one of the most written pieces of code - Hello World

```cpp
#include <iostream>
int main() {
	std::cout<<"Hello World :)\n";
}
```
- Besides greeting the world, it also does one more thing: it implicitly _returns `0`_ when run successfully (if you are acquainted with the shell, you may already realise how to exploit this)

Create a new file: `./CMakeLists.txt`

- This is a **CMake (project) script**
- Each project must have such a script at its root
- A project may contain other projects as subdirectories (advanced usage, not part of this post)

Add the following lines to the script, in order:

```cmake
cmake_minimum_required(VERSION 3.3)
```

- This establishes a minimum CMake version requirement for the project

```cmake
project(hello)
```

- This declares a new CMake project, it is just a name, but is conventionally also used as the name of the executable

```cmake
add_executable(${PROJECT_NAME} main.cpp)
```

- This instructs CMake to construct an executable **target** called `hello` (`${PROJECT_NAME}`, set above) using one source file: `main.cpp`

```cmake
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
```

- This enables the C++17 standard for all source files in this project
- `PRIVATE` properties of a target do not propagate to others that link to it (nothing links to this target, so here it's just a matter of satisfying CMake's syntax)

## Debugger

WIP
