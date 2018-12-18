set(PROJECT "HornetAlg")
project(${PROJECT} CXX)

cmake_minimum_required(VERSION 3.5)
FIND_PACKAGE(CUDA REQUIRED)

add_subdirectory(../hornet build)

include_directories(include)
include_directories(../primitives)
include_directories(../hornet/include)
include_directories(../externals/cub-1.8.0)
include_directories(../externals/cpp-btree-master)
include_directories(../xlib/include)

include(../compiler-util/CMakeLists.txt)

#-------------------------------------------------------------------------------

file(GLOB_RECURSE CU_SRCS ${PROJECT_SOURCE_DIR}/src/*)
file(GLOB_RECURSE CPP_SRCS ${PROJECT_SOURCE_DIR}/externals/xlib/src/*)

cuda_add_library(hornetAlg ${CU_SRCS})
#-------------------------------------------------------------------------------

cuda_add_executable(bfs      test/BFSTest.cu)
cuda_add_executable(bfs2     test/BFSTest2.cu)
cuda_add_executable(brim     test/BrimTest.cu)
cuda_add_executable(cc       test/CCTest.cu)
cuda_add_executable(spmv     test/SpMVTest.cu)
cuda_add_executable(sssp     test/SSSPTest.cu)
cuda_add_executable(katz     test/KatzTest.cu)
cuda_add_executable(dyn_katz test/KatzDynamicTest.cu)
cuda_add_executable(triangle test/TriangleTest.cu)
cuda_add_executable(triangle2 test/TriangleTest2.cu)
cuda_add_executable(clus-coeff test/ClusCoeffTest.cu)

cuda_add_executable(pr test/PageRankTest.cu)

target_link_libraries(bfs      hornetAlg hornet)
target_link_libraries(bfs2     hornetAlg hornet)
target_link_libraries(brim     hornetAlg hornet)
target_link_libraries(cc       hornetAlg hornet)
target_link_libraries(spmv     hornetAlg hornet)
target_link_libraries(sssp     hornetAlg hornet)
target_link_libraries(katz     hornetAlg hornet)
target_link_libraries(dyn_katz hornetAlg hornet)
target_link_libraries(triangle hornetAlg hornet)
target_link_libraries(triangle2 hornetAlg hornet)
target_link_libraries(clus-coeff hornetAlg hornet)
target_link_libraries(pr hornetAlg hornet)