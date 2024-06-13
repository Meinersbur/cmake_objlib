
add_custom_command(
  OUTPUT hello.o
  COMMAND "${CMAKE_CXX_COMPILER}" hello.cpp -c -o hello.o
)

SET_SOURCE_FILES_PROPERTIES(
  hello.o
  PROPERTIES
    EXTERNAL_OBJECT true
    GENERATED true
)


#add_library(myobjectlib OBJECT dummy.cpp hello.o)
add_library(myobjectlib OBJECT IMPORTED)
set_property(TARGET myobjectlib PROPERTY IMPORTED_OBJECTS hello.o)
