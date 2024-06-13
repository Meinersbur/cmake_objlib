
add_custom_command(
  OUTPUT hello.o
  COMMAND "${CMAKE_CXX_COMPILER}"
)

add_library(myobjectlib OBJECT hello.o)
