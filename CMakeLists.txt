cmake_minimum_required(VERSION 3.10)

# set project name
project(AlpacaPiHQ)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

find_package(Threads)
find_package(ZLIB)
#find_package(OpenSSL)

if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()

find_package( Boost 1.70 COMPONENTS system thread REQUIRED )

#target_include_directories(${Boost_INCLUDE_DIR})

# add executable
add_executable(${PROJECT_NAME}-exe
    src/main.cpp
    include/crow_all.h
)

target_include_directories(${PROJECT_NAME}-exe PUBLIC ${PROJECT_SOURCE_DIR}/include ${Boost_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME}-exe
    Threads::Threads
    ZLIB::ZLIB
)