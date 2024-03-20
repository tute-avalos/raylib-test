cmake_minimum_required(VERSION 3.28.3)

project(raylib_test LANGUAGES C)
set(CMAKE_C_STANDARD 99)
set(CMAKE_BUILD_TYPE "Debug")

# copia el binario resultado final para encontrarlo facilmente
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# Se obtiene la dependencia a través de CMake :)
include(FetchContent)
FetchContent_Declare(raylib
    GIT_REPOSITORY https://github.com/raysan5/raylib.git
    GIT_TAG 5.0)
FetchContent_MakeAvailable(raylib)

add_subdirectory(src)
add_subdirectory(include)
add_executable(${PROJECT_NAME} ${SRC_FILES})

# bibliotecas a linkear: raylib m (math) y pthread 
target_link_libraries(${PROJECT_NAME} raylib m pthread) # GL dl rt X11

target_include_directories(${PROJECT_NAME} PRIVATE ${INC_DIRS})
