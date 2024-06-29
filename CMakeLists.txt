cmake_minimum_required(VERSION 3.0)
project(hardware-effects-gpu)

find_package(CUDA REQUIRED)
message(STATUS "Found CUDA version: ${CUDA_VERSION}")

# generate compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "")
# set `-arch` for nvcc
set(CMAKE_CUDA_ARCHITECTURES "90")
set(CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} -arch=sm_${CMAKE_CUDA_ARCHITECTURES} -g -lineinfo -O0")
set(CMAKE_CUDA_COMPILER ${CUDA_TOOLKIT_ROOT_DIR}/bin/nvcc)
enable_language(CUDA)

add_subdirectory(bank-conflicts)
add_subdirectory(memory-coalescing)
add_subdirectory(shared-memory-limit)
