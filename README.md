# QuickWatch

QuickWatch is a github repository where I will store some of my libraries that I plan to develop towards my own web server mostly from scratch.

## Usage

Right now, the way you use this solution is to build it and run the unit tests for the various libraries. There is currently 2 main ways to do this:

1. Use [CTest](https://cmake.org/cmake/help/latest/module/CTest.html/)
2. Run individual unit test runners directly (e.g. `build/Uri/test/Debug/UriTests.exe`)

## Recommended Toolchains and Supported Platforms

* Windows — [Visual Studio](https://www.visualstudio.com/) (MSVC)
* Linux — clang or gcc
* MacOS — Xcode (clang)

## Building

### Prerequisites

* [CMake](https://cmake.org/) version 3.8 or newer
* C++11 toolchain compatible with CMake for your development platform (e.g. [Visual Studio](https://www.visualstudio.com/) on Windows)

### Build System Generation

```console
$ mkdir build
$ cd build
$ cmake -G "Visual Studio 16 2019" -A "x64" ..
```

### Compiling, linking, etc..

```console
$ cd build
$ cmake --build . --config Release
```

<!-- — -->