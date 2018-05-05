
#
# Copyright (C) The Android Open Source Project
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ${CMAKE_SOURCE_DIR}/../../../../distribution)


add_library(lib_gperf SHARED IMPORTED)
set_target_properties(lib_gperf PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/gperf/lib/${ANDROID_ABI}/libgperf.so)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

add_library(mydemo-libs SHARED
            mydemo.cpp)

target_include_directories(mydemo-libs PRIVATE
                           ${distribution_DIR}/gperf/include)

target_link_libraries(mydemo-libs
                      android
                      lib_gperf
                      log)
set_target_properties(mydemo-libs
                      PROPERTIES
                       LIBRARY_OUTPUT_DIRECTORY
                        "${CMAKE_CURRENT_SOURCE_DIR}/../../libs/${ANDROID_ABI}")
