# set a minimum CMake version required
cmake_minimum_required(VERSION 2.4)

# start a new CMake project
project(HelloWorld)

# create build target app
add_executable(app hello.cpp)