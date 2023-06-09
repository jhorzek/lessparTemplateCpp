cmake_minimum_required(VERSION 3.20.0)

# define project:
project(testDocumentation VERSION 1.0)

# specify dependencies:
find_package(Armadillo REQUIRED)
find_package(LAPACK REQUIRED)
find_package(BLAS REQUIRED)

# including lesstimate
set(lesstimate_DIR ${CMAKE_CURRENT_LIST_DIR}/include/lesstimate)
find_package(lesstimate CONFIG REQUIRED)

# set compiler settings
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# we want to use lesstimate without Rcpp -> set USE_R=0
#add_definitions(-DUSE_R=0)

# create target:
add_executable(${PROJECT_NAME} "linear_regression.cpp")

# include armadillo
target_include_directories(${PROJECT_NAME} PRIVATE ${ARMADILLO_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PRIVATE ${ARMADILLO_LIBRARIES} PRIVATE lesstimate::lesstimate LAPACK::LAPACK BLAS::BLAS)
