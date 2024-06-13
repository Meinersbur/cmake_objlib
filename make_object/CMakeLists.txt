
add_custom_command(
  OUTPUT "hello${CMAKE_CXX_OUTPUT_EXTENSION}"
  COMMAND "${CMAKE_CXX_COMPILER}" hello.cpp -c -o "hello${CMAKE_CXX_OUTPUT_EXTENSION}"
)

# "dummy.cpp" is added so CMake can determine the linker to use,
# Alternatively, the LINKER_LANGUAGE property can be set explicitly.
# https://cmake.org/cmake/help/latest/prop_tgt/LINKER_LANGUAGE.html
# Since OBJECT libraries don't require linking, this can be considered a CMake bug.
# Same approach is used in LLVM already, e.g. https://github.com/llvm/llvm-project/blob/main/clang/tools/clang-shlib/clang-shlib.cpp
add_library(myobjectlib OBJECT dummy.cpp "hello${CMAKE_CXX_OUTPUT_EXTENSION}")

# CMake ignores object files added to OBJECT libraries (in contrast to other artifact types such as executables).
# https://gitlab.kitware.com/cmake/cmake/-/issues/21709
# Workaround by adding the object file as linker option.
target_link_options(myobjectlib INTERFACE "${CMAKE_CURRENT_BINARY_DIR}/hello${CMAKE_CXX_OUTPUT_EXTENSION}")

# Alternative approaches:
#  * Use a static library and --whole-archive to ensure it is linked into the target.
#  * Add "${CMAKE_CURRENT_BINARY_DIR}/hello${CMAKE_CXX_OUTPUT_EXTENSION}" to all dependees sources
