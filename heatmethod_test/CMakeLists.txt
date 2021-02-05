cmake_minimum_required(VERSION 3.1...3.18)
project(TEST VERSION 0.1.0)

# CGAL and its components
find_package(CGAL QUIET COMPONENTS)
if ( NOT CGAL_FOUND )
  message(STATUS "This project requires the CGAL library, and will not be compiled.")
  return()
endif()

# include helper file
include( ${CGAL_USE_FILE} )

# Boost and its components
find_package( Boost REQUIRED )
if ( NOT Boost_FOUND )
  message(STATUS "This project requires the Boost library, and will not be compiled.")
  return()
endif()

# Eigen
set(EIGEN3_INCLUDE_DIR D:/eigen-3.3.9)
find_package(Eigen3 3.3.0)
include(CGAL_Eigen_support)

if (NOT TARGET CGAL::Eigen_support)
  message(STATUS "This project requires the Eigen library (3.3 or greater), and will not be compiled.")
  return()
endif()

include_directories( BEFORE include )

add_executable(TEST main.cpp)
target_link_libraries(TEST ${CGAL_LIBS})
target_link_libraries(TEST CGAL::Eigen_support)