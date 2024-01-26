cmake_minimum_required(VERSION 3.5) # CMake install : https://cmake.org/download/
project(ffplayer)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
aux_source_directory(./src srcs)
set(CMAKE_CXX_STANDARD 17)
# Specify MSVC UTF-8 encoding   
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

include_directories(
    ${PROJECT_SOURCE_DIR}/include 
)

include_directories(
    ${PROJECT_SOURCE_DIR}/SDL2/include 
)

link_directories(${PROJECT_SOURCE_DIR}/lib)
link_directories(${PROJECT_SOURCE_DIR}/SDL2/lib/x64)

######### for build dll #########
SET(TARGET "ffplayer")
ADD_LIBRARY(ffplayer SHARED ${srcs})
SET(EXECUTABLE_OUTPUT_PATH "${PROJECT_SOURCE_DIR}/lib")
SET(LIBRARY_OUTPUT_PATH "${PROJECT_SOURCE_DIR}/lib")
######### for build dll #########

# add_executable(${PROJECT_NAME}
#      # If you need a terminal for debug, please comment this statement 
#     ${srcs} 
# ) 
target_link_libraries(${PROJECT_NAME} SDL2 avcodec avformat avutil swresample swscale swscale postproc avfilter)
