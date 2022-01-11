# C++ with CMAKE
The most basic project is an executable built from source code files. 
For simple projects, a three line `CMakeLists.txt` file is all that is required. Inside this file are all commands for CMAKE. 

You can build and run our project now. First, run the cmake executable (or cmake-gui) to configure the project and then build it with your chosen build tool.

Move to the CMake source code tree and create a build directory:
```bash
mkdir build
```
Next, navigate to the build directory and run CMake to configure the project and generate a native build system:
```bash
cd build
cmake ..
```
Then call that build system to actually compile/link the project:
```bash
cmake --build .
```

## Version Numbering and Header Files
Provide the executable and project with a version number, using CMakeLists.txt provides more flexibility. This can be done by using the `VERSION` append to the project name.
```cmake
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(HelloWorld VERSION 1.0)
```

You can also configure header files to pass version numbers to the source code. Here a header file `Hello.h.in` will be read and the version numbers passed to get `Hello.h`
```bash
configure_file(Hello.h.in Hello.h)
```
As the configured file will be written into the binary tree, add that directory to the list of paths to search for include files.
```bash
target_include_directories(HelloWorld PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )
```
When CMake configures header files the values inside `@...@` will be replaced.

## Specify the C++ Standard
Sometimes you need to explicitly state in the CMake code that it should use the correct flags. The easiest way to enable support for a specific C++ standard in CMake is by using the `CMAKE_CXX_STANDARD` variable. Make sure to add the `CMAKE_CXX_STANDARD` declarations above the call to `add_executable`.
```cmake
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(HelloWorld VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```

## Rebuild
Build our project again. As you already created the bild directory skip this step and proceed:
```bash
cd build
cmake --build .
```