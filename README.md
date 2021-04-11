# cmake-tutorial
CMake is an extremely versatile C++ project build system that makes development much easier no matter the system you are working in. If you are unfamiliar with CMake you can see the general components of a CMakeLists file and how to start a project from [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html).

## Project Setup

```cmake
cmake_minimum_required(VERSION 3.10)

# set the project name
project(Tutorial)

# add the executable
add_executable(Tutorial tutorial.cxx)
```
