cmake_minimum_required(VERSION 3.28.3)

PROJECT(raylib_test)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_BUILD_TYPE "Debug")

add_subdirectory(src)
add_subdirectory(include)
add_executable(${PROJECT_NAME} ${SRC_FILES})

# Acá se pone el directorio relativo donde está la versión compilada de raylib
#  en mi caso, es en la carpeta inmediata superior...
add_library(raylib STATIC IMPORTED)
set_target_properties(raylib PROPERTIES
  IMPORTED_LOCATION "${CMAKE_SOURCE_DIR}/../raylib/build/raylib/libraylib.a"
  INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}/../raylib/build/raylib/include/"
)

# bibliotecas a linkear: raylib m (math) y pthread 
target_link_libraries(raylib_test raylib m pthread GL dl rt X11) # also adds the required include path

target_include_directories(${PROJECT_NAME} PRIVATE ${INC_DIRS})
