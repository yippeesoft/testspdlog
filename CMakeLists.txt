# Copyright(c) 2019 spdlog authors Distributed under the MIT License
# (http://opensource.org/licenses/MIT)

cmake_minimum_required(VERSION 3.10)
project(spdlog_examples CXX)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
if(DEFINED xxx AND xxx GREATER 20)

endif()
set(CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer ")

set(CMAKE_LINKER_FLAGS
    "${CMAKE_LINKER_FLAGS} -fsanitize=address  -lasan -lstdc++ ")

set(CMAKE_EXE_LINKER_FLAGS
    "${CMAKE_EXE_LINKER_FLAGS} -fsanitize=address  -lasan -lstdc++ ")

if(NOT TARGET spdlog)
  # Stand-alone build
  find_package(spdlog REQUIRED)
endif()

# ---------------------------------------------------------------------------------------
# Example of using pre-compiled library
# ---------------------------------------------------------------------------------------
add_executable(example example.cpp)
target_link_libraries(example PRIVATE spdlog::spdlog)

# ---------------------------------------------------------------------------------------
# Example of using header-only library
# ---------------------------------------------------------------------------------------
if(SPDLOG_BUILD_EXAMPLE_HO)
  add_executable(example_header_only example.cpp)
  target_link_libraries(example_header_only PRIVATE spdlog::spdlog_header_only)
endif()
