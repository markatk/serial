add_executable(serial_example serial_example.cc)
add_dependencies(serial_example ${PROJECT_NAME})
target_include_directories(serial_example PRIVATE ../include)
target_link_libraries(serial_example ${PROJECT_NAME})