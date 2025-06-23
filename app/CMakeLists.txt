
add_executable(custom_baudrate
        "custom_baudrate/main.cpp"
)

add_executable(simple_grabber
        "simple_grabber/main.cpp"
)

add_executable(ultra_simple
        "ultra_simple/main.cpp"
)

target_link_libraries(custom_baudrate PRIVATE rplidar)
target_link_libraries(simple_grabber PRIVATE rplidar)
target_link_libraries(ultra_simple PRIVATE rplidar)
