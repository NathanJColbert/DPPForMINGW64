# DPP For MINGW64

## Description

A preset project structure for making discord bots with DPP (Discord plus plus) on windows using the MINGW64 environment, CMake and ninja. (If you like the linux environment but are forced to use windows!). The source code for dpp is present and modifiable.

## Table of Contents

- [Expected Architecture](#expected-architecture)
- [Dependencies](#dependencies)
- [Setup](#setup)
- [Build & Run](#build--run)
- [Customization](#customization)

## Expected Architecture

Using windows with MINGW64 environment. CMake and ninja for the build system.

## Dependencies

Using MINGW64 is super easy! Make sure you are running the right MYSYS2 executable (MINGW64). DPP uses opus, fmt and gcc (for the compiler).
```bash
pacman -Syu
pacman -S \
    mingw-w64-x86_64-cmake \
    mingw-w64-x86_64-gcc \
    mingw-w64-x86_64-fmt \
    mingw-w64-x86_64-opus \
    git
```

## Setup

```bash
# Clone the repository (with submodules - dpp)
git clone --recurse-submodules HTTPGoesHereLol
cd DPPForMINGW64

# OR
git clone HTTPGoesHereLol
cd DPPForMINGW64
git submodule update --init --recursive
```

## Build & Run

```bash
# Make a build folder
mkdir build
cd build

# Setup CMake
cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Release

# Build
ninja

# Run
./MyBot.exe
```

## Customization

To add your own source and header files, make sure your header files are in the include directory and your source files listed in the CMakeLists
```bash
add_executable(MyBot
    src/main.cpp
    src/mySecondSource.cpp
)
```
OR change the CMakeLists to glob the src directory (Remember to re-run 'cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Release' when adding more source files)
```bash
# uncomment this
file(GLOB SRC_FILES src/*.cpp)
add_executable(MyBot ${SRC_FILES})

# remove / comment this
add_executable(MyBot
    src/main.cpp
    # Add *.cpp files here
)
```