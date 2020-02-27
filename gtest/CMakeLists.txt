cmake_minimum_required(VERSION 3.10.0)

project(GTest LANGUAGES CXX)

set(GTEST_PATH ${ANDROID_NDK}/sources/third_party/googletest)

add_library(gtest
  STATIC
    ${GTEST_PATH}/src/gtest-all.cc
)

target_include_directories(gtest
  PRIVATE
    ${GTEST_PATH}
  PUBLIC
    ${GTEST_PATH}/include
)
