cmake_minimum_required(VERSION 3.16)
project(LibraryManagementSystem VERSION 1.0 LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Include selected source files
add_library(lms
    src/library.c
)

# Include directories
target_include_directories(lms PUBLIC "${PROJECT_SOURCE_DIR}/src")

# Create executable
add_executable(lms_executable src/main.c)
