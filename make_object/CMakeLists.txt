
add_custom_command(
  OUTPUT hello.o
  COMMAND "${CMAKE_CXX_COMPILER}" hello.cpp -c -o hello.o
)

add_library(myobjectlib OBJECT dummy.cpp hello.o)
