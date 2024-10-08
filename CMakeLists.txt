cmake_minimum_required(VERSION 3.14)
project(sample_cpp_project)

include_directories(include)

add_executable(main main.cpp src/my_add.cpp)

include(FetchContent)
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG v1.15.2
)
FetchContent_MakeAvailable(googletest)

enable_testing()
add_executable(tests test_add.cpp src/my_add.cpp)
target_link_libraries(tests gtest_main)

include(GoogleTest)
gtest_discover_tests(tests)

FetchContent_Declare(
    benchmark
    GIT_REPOSITORY https://github.com/google/benchmark.git
    GIT_TAG        main
)

FetchContent_MakeAvailable(benchmark)

add_executable(benchmark_add benchmark_add.cpp src/my_add.cpp)
target_link_libraries(benchmark_add benchmark::benchmark)
