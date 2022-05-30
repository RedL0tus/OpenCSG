cmake_minimum_required(VERSION 3.11)
project(OpenCSG VERSION 1.5.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB_RECURSE SOURCE_FILES
	"${CMAKE_SOURCE_DIR}/src/*.cpp"
	"${CMAKE_SOURCE_DIR}/src/*.h"
	"${CMAKE_SOURCE_DIR}/include/*.h"
	"${CMAKE_SOURCE_DIR}/RenderTexture/*.cpp"
	"${CMAKE_SOURCE_DIR}/RenderTexture/*.h"
)

add_library(opencsg SHARED "${SOURCE_FILES}")
set_target_properties(opencsg PROPERTIES SOVERSION 1.4)
target_include_directories(opencsg PRIVATE
	"${CMAKE_SOURCE_DIR}"
	"${CMAKE_SOURCE_DIR}/include"
)

find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)
find_package(OpenGL REQUIRED)

target_link_libraries(opencsg PRIVATE GLEW::GLEW)
target_link_libraries(opencsg PRIVATE GLUT::GLUT)
target_link_libraries(opencsg PRIVATE OpenGL::OpenGL)

install(TARGETS opencsg DESTINATION lib)
install(FILES "${CMAKE_SOURCE_DIR}/include/opencsg.h" DESTINATION include)
