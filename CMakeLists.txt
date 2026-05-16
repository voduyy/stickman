cmake_minimum_required(VERSION 3.16)
project(Stickman)

set(CMAKE_CXX_STANDARD 17)

add_executable(game main.cpp)

target_include_directories(game PRIVATE
    ${CMAKE_SOURCE_DIR}/libs/SDL3/include
)

target_link_directories(game PRIVATE
    ${CMAKE_SOURCE_DIR}/libs/SDL3/lib
)

target_link_libraries(game PRIVATE SDL3)

# Copy SDL3.dll vào thư mục build (Windows only)
if(WIN32)
    add_custom_command(TARGET game POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_SOURCE_DIR}/libs/SDL3/bin/SDL3.dll"
        $<TARGET_FILE_DIR:game>
    )
endif()