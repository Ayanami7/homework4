cmake_minimum_required(VERSION 3.5)

project(homework4 VERSION 1.0 LANGUAGES CXX)
set(MAIN_EXE main)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 确保生成的exe不依赖于动态链接库
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")

find_package(Qt6 REQUIRED COMPONENTS Core)
find_package(Qt6 REQUIRED COMPONENTS Widgets)

add_subdirectory(ext/googletest)

add_executable(${MAIN_EXE}
    src/scene.hpp
    src/scene.cpp
    src/mainwindow.hpp
    src/main.cpp
    src/manager.hpp
    src/manager.cpp
    src/mainwindow.cpp
)

target_include_directories(${MAIN_EXE}
PUBLIC
    ${PROJECT_SOURCE_DIR}/src
)

target_link_libraries(${MAIN_EXE} PRIVATE Qt6::Core)
target_link_libraries(${MAIN_EXE} PRIVATE Qt6::Widgets)


#添加调试程序
add_executable(test1
    test/test1.cpp
    src/manager.hpp
    src/manager.cpp
    src/scene.hpp
    src/scene.cpp
    src/mainwindow.hpp
    src/mainwindow.cpp
)
target_include_directories(test1 PRIVATE ${PROJECT_SOURCE_DIR}/src)
target_link_libraries(test1 PRIVATE GTest::gtest GTest::gtest_main)
target_link_libraries(test1 PRIVATE Qt6::Core)
target_link_libraries(test1 PRIVATE Qt6::Widgets)
