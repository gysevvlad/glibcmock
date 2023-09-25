add_executable(glibc_mock_test
  got_hook_test.cc
  sample1.cc 
  sample2.cc
  sample3.cc
  test_main.cc)

set_target_properties(glibc_mock_test
  PROPERTIES
    POSITION_INDEPENDENT_CODE FALSE)

target_link_libraries(glibc_mock_test
  glibcmock
  GTest::gtest
  GTest::gmock
  GTest::gmock_main)

include(GoogleTest)

gtest_discover_tests(glibc_mock_test)
