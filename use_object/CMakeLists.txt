

add_executable(hello other_sources.cpp $<TARGET_OBJECTS:myobjectlib>)
target_link_libraries(hello PRIVATE myobjectlib)
