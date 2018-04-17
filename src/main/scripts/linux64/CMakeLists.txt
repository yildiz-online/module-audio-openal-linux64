cmake_minimum_required (VERSION 3.0.0)

project (yildiz_native_openal)

set(CMAKE_CXX_FLAGS "-O2 -fPIC -std=gnu++11")

find_package(OpenAL REQUIRED)
find_package(PhysFS REQUIRED)
find_package(Java REQUIRED)
find_package(JNI REQUIRED)
find_package(LibSndFile REQUIRED)

include_directories(${OPENAL_INCLUDE_DIR})
include_directories(${PHYSFS_INCLUDE_DIR})
include_directories("java/include")
include_directories("java/include/linux")
include_directories(${LIBSNDFILE_INCLUDE_DIR})

file(
        GLOB_RECURSE
        source_files
        ${CMAKE_SOURCE_DIR}/../../c++/*.cpp
        ${CMAKE_SOURCE_DIR}/../../includes/*.hpp
        ${CMAKE_SOURCE_DIR}/../../includes/*.h
)

add_library(yildizopenal SHARED ${source_files})

target_link_libraries(yildizopenal ${OPENAL_LIBRARY})
target_link_libraries(yildizopenal ${PHYSFS_LIBRARY})
target_link_libraries(yildizopenal ${LIBSNDFILE_LIBRARY})
