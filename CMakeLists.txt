CMAKE_MINIMUM_REQUIRED(VERSION 3.5)

PROJECT(homework1)
SET(CMAKE_CXX_STANDARD 14)

#set build type
set(CMAKE_BUILD_TYPE Debug)

#add path for find scripts
include(${PROJECT_SOURCE_DIR}/cmake/test_median.cmake)

#include CTest so we can run unit tests with CMake
include(CTest)

## Major project
INCLUDE_DIRECTORIES(include)

set( MEDIANCALCULATORS_SRC src/median_calculator_base.cpp
                           src/sorting_median_calculator.cpp
                           src/lap_timer.cpp )
add_library( median_calculators ${MEDIANCALCULATORS_SRC} )

ADD_EXECUTABLE( test_median_computation test/test_median_computation.cpp )
TARGET_LINK_LIBRARIES( test_median_computation median_calculators )

ADD_EXECUTABLE( test_median_computation_speed test/test_median_computation_speed.cpp )
TARGET_LINK_LIBRARIES( test_median_computation_speed median_calculators )

test_median(0 SORTED)

# TODO: add your implementation into CTest cases. We have perpared `test_median`
#   helper function for you:
#
#   test_median(method_idx method_name)
#
#   Arguments:
#     - method_idx (int): specify the index of your method in `main` function,
#           which will be passed as `argv[1]` to `main`;
#     - method_name (string): specify the name of your method in `main` function,
#           used as subfix of CTest executables;
#
#   Examples:
#     test_median(1 QUICK_SELECT)

# test_median(1 QUICK_SELECT)
