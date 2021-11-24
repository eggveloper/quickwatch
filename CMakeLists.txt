#####################
#    Quick Watch    #
# © 2021 Callum Ali #
#####################
#   DON'T MODIFY!   #
#####################

cmake_minimum_required(VERSION 3.8)
project(QuickWatch C CXX)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

enable_testing()

get_directory_property(ParentDirectory PARENT_DIRECTORY)

if(ParentDirectory STREQUAL "")
    if(MSVC)
        option(RUNTIME_STATIC_LINKAGE "Link with runtime library statically [default: OFF]" OFF)
    endif(MSVC)

    if(MSVC AND RUNTIME_STATIC_LINKAGE)
        foreach(flag
            CMAKE_C_FLAGS
            CMAKE_CXX_FLAGS
            CMAKE_C_FLAGS_DEBUG
            CMAKE_CXX_FLAGS_DEBUG
            CMAKE_C_FLAGS_RELEASE
            CMAKE_CXX_FLAGS_RELEASE
            CMAKE_C_FLAGS_MINSIZEREL
            CMAKE_CXX_FLAGS_MINSIZEREL
            CMAKE_C_FLAGS_RELWITHDEBINFO
            CMAKE_CXX_FLAGS_RELWITHDEBINFO
        )
        
        if (${flag} MATCHES "/MD")
            string(REGEX REPLACE "/MD" "/MT" ${flag} "${${flag}}")
        endif(${flag} MATCHES "/MD")
        endforeach(flag)
    endif(MSVC AND RUNTIME_STATIC_LINKAGE)

    if(RUNTIME_STATIC_LINKAGE)
        set(gtest_force_shared_crt OFF CACHE BOOL "Use shared (DLL) run-time lib even when Google Test is built as a static lib." FORCE)
    else(RUNTIME_STATIC_LINKAGE)
        set(gtest_force_shared_crt ON CACHE BOOL "Use shared (DLL) run-time lib even when Google Test is built as a static lib." FORCE)
    endif()

    set_property(GLOBAL PROPERTY USE_FOLDERS ON)

    set(CMAKE_SKIP_BUILD_RPATH FALSE)
    set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)

    if(APPLE)
        set(CMAKE_INSTALL_RPATH "@loader_path")
    elseif(APPLE)
        set(CMAKE_INSTALL_RPATH "\$ORIGIN")
    endif()

    set(CMAKE_DEBUG_POSTFIX "")

    add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_SCL_SECURE_NO_WARNINGS)

    set(BUILD_GTEST ON CACHE BOOL "Builds googletest subproject" FORCE)
    set(BUILD_GMOCK OFF CACHE BOOL "Builds googlemock subproject" FORCE)
    
    add_subdirectory(googletest)
    set_target_properties(gtest gtest_main PROPERTIES
        FOLDER Libraries
    )

    add_subdirectory(Uri)
endif(ParentDirectory STREQUAL "")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})