cmake_minimum_required(VERSION 3.10)
project(sample
  LANGUAGES CXX
)
include(extern_lib.cmake)
set(SRC_LIST
	camera.cpp
	cmd.cpp
	data.cpp
	display.cpp
	sample.cpp	
	temperature.cpp
)
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/libir_sample
)

link_directories(${CMAKE_CURRENT_SOURCE_DIR}/libs/Win32)

add_executable(sample ${SRC_LIST})
add_compile_definitions(IMAGE_AND_TEMP_OUTPUT)
add_compile_definitions(_CRT_SECURE_NO_WARNINGS)

if(CMAKE_CL_64)
    target_link_libraries(sample
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/libiruvc.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/libirtemp.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/libirprocess.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/libirparse.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/pthreadVC2.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/x64/opencv_world401d.lib
    )
else()
    target_link_libraries(sample
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/Win32/libiruvc.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/Win32/libirtemp.lib
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/Win32/libirprocess.lib
    )
endif()
