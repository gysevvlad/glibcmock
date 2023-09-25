cmake_minimum_required(VERSION 3.27)

project(glibcmock)

add_library(glibcmock STATIC)

target_sources(glibcmock
  PRIVATE
    got_hook.cc
  PUBLIC
    FILE_SET "public_headers"
    TYPE "HEADERS"
    FILES
      got_hook.h)

find_package(GTest REQUIRED)

target_link_libraries(glibcmock
  GTest::gtest)

target_compile_options(glibcmock
  PUBLIC
    "-fno-pie")

target_link_options(glibcmock
  PUBLIC
    "-no-pie")

include(CPack)

install(
    TARGETS glibcmock
    EXPORT glibcmockTargets
    FILE_SET public_headers)

install(
    EXPORT glibcmockTargets
    FILE glibcmockTargets.cmake
    NAMESPACE glibcmock::
    DESTINATION lib/cmake/glibcmock)

include(CMakePackageConfigHelpers)

configure_package_config_file(
    cmake/Config.cmake.in
    glibcmockConfig.cmake
    INSTALL_DESTINATION lib/cmake/glibcmock)

install(
    FILES
    ${CMAKE_CURRENT_BINARY_DIR}/glibcmockConfig.cmake
    DESTINATION lib/cmake/glibcmock)

include(CTest)

if (BUILD_TESTING)
  add_subdirectory(test)
endif()
