cmake_minimum_required(VERSION 3.14)

# https://github.com/xmos/lib_xs3_math/issues/78
cmake_policy(SET CMP0057 NEW)

include(cmake/CPM.cmake)

project(xmos-lib_i2c)

## CMake configuration stuff
enable_language( C CXX ASM )
set( CMAKE_CXX_STANDARD           11  )
set( CMAKE_CXX_STANDARD_REQUIRED  ON  )
set( CMAKE_CXX_EXTENSIONS         OFF )

string(REPLACE "-MD" "-MMD" CMAKE_DEPFILE_FLAGS_C ${CMAKE_DEPFILE_FLAGS_C})

# add_compile_options( ${COMPILE_FLAGS} )

## Add libs and apps directory
add_subdirectory( lib_i2c )
# add_subdirectory( app ) # not needed

## Add and link the library
add_library(
    lib_i2c_general INTERFACE
)

target_link_libraries(
    lib_i2c_general INTERFACE 
        lib_i2c
)

add_library(i2c::lib_i2c ALIAS lib_i2c_general)