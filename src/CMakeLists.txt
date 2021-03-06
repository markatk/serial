## Sources
set(serial_SRCS
        serial.cc
        ../include/serial/serial.h
        ../include/serial/v8stdint.h
        )
if(APPLE)
    # If OSX
    list(APPEND serial_SRCS impl/unix.cc)
    list(APPEND serial_SRCS impl/list_ports/list_ports_osx.cc)
elseif(UNIX)
    # If unix
    list(APPEND serial_SRCS impl/unix.cc)
    list(APPEND serial_SRCS impl/list_ports/list_ports_linux.cc)
else()
    # If windows
    list(APPEND serial_SRCS impl/win.cc)
    list(APPEND serial_SRCS impl/list_ports/list_ports_win.cc)
endif()

## Add serial library
add_library(${PROJECT_NAME} ${serial_SRCS})

target_include_directories(${PROJECT_NAME} PUBLIC ../include)

if(APPLE)
    target_link_libraries(${PROJECT_NAME} ${FOUNDATION_LIBRARY} ${IOKIT_LIBRARY})
elseif(UNIX)
    target_link_libraries(${PROJECT_NAME} rt pthread)
else()
    target_link_libraries(${PROJECT_NAME} setupapi)
endif()

## Install executable
install(TARGETS ${PROJECT_NAME}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        )

## Install headers
install(FILES include/serial/serial.h include/serial/v8stdint.h
        DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}/serial)