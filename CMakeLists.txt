cmake_minimum_required(VERSION 3.10...3.21)
project(rocket CXX)

if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    set(ROCKET_MASTER_PROJECT ON)
else()
    set(ROCKET_MASTER_PROJECT OFF)
endif()

option(ROCKET_BUILD_EXAMPLES "Build examples" ${ROCKET_MASTER_PROJECT})

# compile defines moved to options
# every feature defaults to on
option(ROCKET_NO_EXCEPTIONS "Disable exceptions" OFF)
option(ROCKET_NO_STABLE_LIST "Disable the stable_list collection" OFF)
option(ROCKET_NO_TIMERS "Disable the set_timeout and set_interval features" OFF)
option(ROCKET_NO_BLOCKING_CONNECTIONS "Disable the connection blocking feature" OFF)
option(ROCKET_NO_QUEUED_CONNECTIONS "Disable the queued connection feature" OFF)
option(ROCKET_NO_SMARTPOINTER_EXTENSIONS "Disable the smart pointer extensions feature" OFF)


# C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# generate compile_commands.json if possible
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_library(rocket INTERFACE)
add_library(rocket::rocket ALIAS rocket)

target_include_directories(rocket INTERFACE ${CMAKE_CURRENT_LIST_DIR}/include)

foreach(
    ROCKET_OPTION
    ROCKET_NO_EXCEPTIONS
    ROCKET_NO_STABLE_LIST
    ROCKET_NO_TIMERS
    ROCKET_NO_BLOCKING_CONNECTIONS
    ROCKET_NO_QUEUED_CONNECTIONS
    ROCKET_NO_SMARTPOINTER_EXTENSIONS)

    if(${ROCKET_OPTION})
        target_compile_definitions(rocket INTERFACE ${ROCKET_OPTION})
    endif()
endforeach()

if(ROCKET_BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()
