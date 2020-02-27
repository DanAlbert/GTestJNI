cmake_minimum_required(VERSION 3.10.0)

project(GTestJNI LANGUAGES CXX)

find_package(gtest CONFIG REQUIRED)

add_library(app
  SHARED
    src/main/cpp/app.cpp
    src/main/cpp/adder.cpp
)

add_library(nativehelper
  INTERFACE
)

target_include_directories(nativehelper
  INTERFACE
    src/main/cpp
)

add_library(gtestjni
  STATIC
    src/main/cpp/gtest_wrapper.cpp
)

target_link_libraries(gtestjni
  PRIVATE
    gtest::gtest
    nativehelper
  PUBLIC
    -uJava_com_android_gtestjni_GtestRunner_nInitialize
    -uJava_com_android_gtestjni_GtestRunner_nRun
)

add_library(apptest
  SHARED
    src/main/cpp/app_test.cpp
)

target_link_libraries(apptest
  PRIVATE
    app
    gtest::gtest
    gtestjni
)
