cmake_minimum_required(VERSION 3.14)
project(VDSProject CXX C)
 set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -fPIC -std=c++11 ${LLVM_CXX_FLAGS} ")

include(FetchContent)
FetchContent_Declare(
        googletest
        # Specify the commit you depend on and update it regularly.
        URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

#set(Boost_INCLUDE_DIR c:/usr/local/include/)
#set(Boost_LIBRARY_DIR C:/Program Files/Boost/boost_1_55_0/libs)
find_package(Boost COMPONENTS system filesystem REQUIRED)
include_directories(${Boost_INCLUDE_DIR})

include_directories(${CMAKE_SOURCE_DIR}/src)
link_directories(${CMAKE_SOURCE_DIR}/src)

include_directories(${CMAKE_SOURCE_DIR}/src/test/)
link_directories(${CMAKE_SOURCE_DIR}/src/test/)

include_directories(${CMAKE_SOURCE_DIR}/src/reachability/)
link_directories(${CMAKE_SOURCE_DIR}/src/reachability/)

include_directories(${CMAKE_SOURCE_DIR}/src/bench/)
link_directories(${CMAKE_SOURCE_DIR}/src/bench/)

include_directories(${CMAKE_SOURCE_DIR}/src/verify/)
link_directories(${CMAKE_SOURCE_DIR}/src/verify/)

add_subdirectory(src)
#add_executable(VDSProject src/main.cpp src/bench/main_bench.cpp src/verify/main_verify.cpp)
add_executable(VDSProject src/main.cpp)
target_link_libraries(VDSProject Manager)




