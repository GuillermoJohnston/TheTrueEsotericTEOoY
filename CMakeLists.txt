cmake_minimum_required(VERSION 3.18)
project(DHL_LOGISTICS)

set(TARGET "server" CACHE STRING "Build target: server or client")

include_directories(include)
include_directories(include/common)

if("${TARGET}" STREQUAL "server")
    add_definitions(-DTARGET_SERVER)
    include_directories(include/server)
    file(GLOB SOURCES
        src/server/*.cpp
        src/common/*.cpp
    )
    add_executable(dhl_server ${SOURCES})

elseif(TARGET STREQUAL "client")
    add_definitions(-DTARGET_CLIENT)
    include_directories(include/client)
    file(GLOB SOURCES
        src/client/*.c
        src/common/*.c
    )
    add_executable(dhl_client ${SOURCES})

else()
    message(FATAL_ERROR "Invalid TARGET. Use -DTARGET=server or -DTARGET=client")
endif()