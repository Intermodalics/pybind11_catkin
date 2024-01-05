cmake_minimum_required(VERSION 3.4)
project(pybind11_catkin)

find_package(catkin REQUIRED)

set(PYBIND11_MINIMUM_REQUIRED_VERSION 2.5.0)
set(PYBIND11_PYTHON_VERSION ${PYTHON_VERSION_STRING})

find_package(pybind11 ${PYBIND11_MINIMUM_REQUIRED_VERSION} QUIET)
if(NOT pybind11_FOUND)
  include(ExternalProject)

  ExternalProject_Add(pybind11_src
    URL "https://github.com/pybind/pybind11/archive/v2.10.3.zip"
    UPDATE_COMMAND ""
    CMAKE_ARGS
      -DPYBIND11_NOPYTHON=TRUE
      -DPYBIND11_TEST=OFF
      -DPYBIND11_INSTALL=ON
      -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
  )
endif()

catkin_package(
  CFG_EXTRAS pybind11_catkin.cmake
)
