
set(sources
        "sl_lidar_driver.cpp"
        "hal/thread.cpp"
        "sl_crc.cpp"
        "sl_serial_channel.cpp"
        "sl_lidarprotocol_codec.cpp"
        "sl_async_transceiver.cpp"
        "sl_tcp_channel.cpp"
        "sl_udp_channel.cpp"

        "dataunpacker/dataunpacker.cpp"
        "dataunpacker/unpacker/handler_capsules.cpp"
        "dataunpacker/unpacker/handler_hqnode.cpp"
        "dataunpacker/unpacker/handler_normalnode.cpp"
)

if (UNIX)
    if (APPLE)
        set(arch "macOS")
    else ()
        set(arch "linux")
    endif ()
else ()
    set(arch "win32")
endif ()

list(APPEND sources
        "arch/${arch}/net_serial.cpp"
        "arch/${arch}/net_socket.cpp"
        "arch/${arch}/timer.cpp"
)

add_library(rplidar ${sources})
target_include_directories(rplidar
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
        PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/dataunpacker/unpacker
)

if (UNIX)
    target_link_libraries(rplidar PRIVATE pthread)
endif ()

set_target_properties(rplidar PROPERTIES POSITION_INDEPENDENT_CODE ON)
