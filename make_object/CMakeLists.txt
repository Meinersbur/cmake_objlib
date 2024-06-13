
add_custom_command(
  OUTPUT "hello${CMAKE_CXX_OUTPUT_EXTENSION}"
  COMMAND "${CMAKE_CXX_COMPILER}" hello.cpp -c -o "hello${CMAKE_CXX_OUTPUT_EXTENSION}"
)


add_library(myobjectlib OBJECT dummy.cpp "hello${CMAKE_CXX_OUTPUT_EXTENSION}")

# https://gitlab.kitware.com/cmake/cmake/-/issues/21709
target_link_options(myobjectlib INTERFACE "${CMAKE_CURRENT_BINARY_DIR}/hello${CMAKE_CXX_OUTPUT_EXTENSION}")
