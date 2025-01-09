cmake_minimum_required(VERSION 3.10)
project(bitfield LANGUAGES C)

# Define the source files
set(BF_SOURCES 
	${CMAKE_CURRENT_SOURCE_DIR}/src/bitfield/8byte.c
	${CMAKE_CURRENT_SOURCE_DIR}/src/bitfield/bitarray.c
	${CMAKE_CURRENT_SOURCE_DIR}/src/bitfield/bitfield.c
	${CMAKE_CURRENT_SOURCE_DIR}/src/canutil/read.c
	${CMAKE_CURRENT_SOURCE_DIR}/src/canutil/write.c
)


# Define common include directories
set(COMMON_INCLUDE_BF
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/src/bitfield
    ${CMAKE_CURRENT_SOURCE_DIR}/src/canutil
)

# Add the UDS library as a static library
add_library(bitfield STATIC ${BF_SOURCES})

# Include directories for UDS
target_include_directories(bitfield PUBLIC ${COMMON_INCLUDE_BF})

# Compiler flags
target_compile_options(bitfield PRIVATE
    -w                  # Disable all warnings
    -std=c99            # Use C99 standard
    -O0                 # No optimization
)

# Set the output directory for the library
set_target_properties(bitfield PROPERTIES 
    ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/lib
)

