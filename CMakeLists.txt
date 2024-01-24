cmake_minimum_required(VERSION 3.5) # CMake install : https://cmake.org/download/
project(ffplayer LANGUAGES C)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# set(CMAKE_PREFIX_PATH "c:/Qt/Qt5.14.2/5.14.2/msvc2017_64") # Qt Kit Dir
set(CMAKE_AUTOUIC ON)
# set(CMAKE_CXX_STANDARD 11)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
# find_package(Qt5 COMPONENTS Widgets Multimedia REQUIRED) # Qt COMPONENTS
aux_source_directory(./src srcs)

# Specify MSVC UTF-8 encoding   
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

include_directories(
    ${PROJECT_SOURCE_DIR}/include 
)

include_directories(
    ${PROJECT_SOURCE_DIR}/SDL2/include 
)


# set(mingw64_includ "C:/msys64/mingw64/include")
# message(STATUS "lkmao:PROJECT_SOURCE_DIR -- ${mingw64_includ}")
# include_directories(
#     ${mingw64_includ}
# )

# set(SDL2_includ "C:/msys64/mingw64/include/SDL2")
# include_directories(
#     ${SDL2_includ}
# )

# message(STATUS "lkmao:PROJECT_SOURCE_DIR -- ${PROJECT_SOURCE_DIR}")
link_directories(${PROJECT_SOURCE_DIR}/lib)
link_directories(${PROJECT_SOURCE_DIR}/SDL2/lib/x64)


add_executable(${PROJECT_NAME}
     # If you need a terminal for debug, please comment this statement 
    ${srcs} 
) 
target_link_libraries(${PROJECT_NAME} SDL2 avcodec avformat avutil swresample swscale swscale postproc avfilter) # Qt5 Shared Library
