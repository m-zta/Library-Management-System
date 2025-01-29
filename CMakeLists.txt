# RUN CMAKE:CONFIGURE AFTER EDITING THIS FILE

cmake_minimum_required(VERSION 3.16)
project(LibraryManagementSystem VERSION 1.0 LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Include selected source files
add_library(lms
    src/library.c
)

# Include directories
target_include_directories(lms PRIVATE "${PROJECT_SOURCE_DIR}/src") # PRIVATE for small projects

# Create executable
add_executable(lms_executable src/main.c)

# Link the library to the executable
target_link_libraries(lms_executable PRIVATE lms)

# Add a testing option
option(ENABLE_TESTS "Enable building tests" OFF)

if (ENABLE_TESTS)
    enable_testing()

    # Add the test executable
    add_executable(test_library tests/test_library.c src/library.c)

    # Include directories for tests
    target_include_directories(test_library PRIVATE "${PROJECT_SOURCE_DIR}/src")

    # Link the CMocka library, consider using Unity instead
    target_link_libraries(test_library PRIVATE cmocka)

    # Add the test executable to CTest
    add_test(NAME test_library COMMAND test_library)
endif()
