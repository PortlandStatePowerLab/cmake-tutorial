# cmake-tutorial
CMake is an extremely versatile C++ project build system that makes development much easier no matter the system you are working in. If you are unfamiliar with CMake you can see the general components of a CMakeLists file and how to start a project from [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html).

## Project Setup

```cmake
cmake_minimum_required(VERSION 3.14)

# project variables
set(PROJECT_VERSION 1.0.0)
set(PROJECT_NAME name)

# This is your project statement. You should always list languages;
project(
  ${PROJECT_NAME}
  VERSION ${PROJECT_VERSION}
  LANGUAGES CXX
)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```
## Fetch Content or Find Package
CMake 3.14 added a very useful *FetchContent()* macro for downloading and installing project dependancies. We try to use this as much as possible, but some dependancies are difficult to include this way so they are just installed within the development environment and included using *find_package()*

```cmake
find_package(Boost REQUIRED)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        master
)

FetchContent_MakeAvailable(googletest)
```

## Add Subdirectories for source files
Once the project variables and dependancies have been declared we point the main CMakeLists to subdirectories that include the source code for our project or the test code for our project. 

```cmake
add_subdirectory(src)
add_subdirectory(tests)
```

## Add Executable
Within your source code directory create another CMakeLists file that sets the project executable and links libraries and include folders to the source code.

```cmake
add_executable(app 
  main.cpp 
  SomeClass.cpp 
  AnotherClass.cpp 
)

target_link_libraries(app PUBLIC 
  Boost::boost 
  pthread
)

target_include_directories(app PUBLIC 
	${Boost_INCLUDE_DIRS}
)
```

## Building and Running
Now that the CMake files have been setup and our code is written it is time to compile and test. From the root directory of the project run the following commands to build/run our program.

```shell
cmake -S . -B build
cmake --build build
./build/src/app
``
