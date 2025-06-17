cmake_minimum_required(VERSION 3.13.4)
project(toy LANGUAGES CXX C)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED YES)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
add_compile_options(-g)

find_package(MLIR REQUIRED CONFIG)
list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")
list(APPEND CMAKE_MODULE_PATH "${MLIR_CMAKE_DIR}")

include(TableGen)
include(AddLLVM)
include(AddMLIR)
include(HandleLLVMOptions)

include_directories(${LLVM_INCLUDE_DIRS} ${MLIR_INCLUDE_DIRS} include/)

add_executable(toy toyc.cpp parser/AST.cpp)
target_link_libraries(toy
  PRIVATE
    LLVMSupport
    MLIRSupport
#   MLIRIR
#   MLIRParser
#   MLIRFuncDialect
#   MLIRArithDialect
)

set(NO_RTTI "-fno-rtti")
add_definitions(${NO_RTTI})