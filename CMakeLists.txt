cmake_minimum_required(VERSION 3.5.1)
project(mw-open-mpi-exec)

add_executable(mw-open-mpi-exec main.cc)
set_target_properties(mw-open-mpi-exec PROPERTIES
        CXX_STANDARD 11
        CXX_STANDARD_REQUIRED ON)


find_package(OpenMP REQUIRED)
if (OPENMP_FOUND)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()
find_package(MPI REQUIRED)

message(STATUS ${MPI_INCLUDE_PATH})
message(STATUS ${MPI_CXX_LIBRARIES})
message(STATUS ${MPI_C_LIBRARIES})
message(STATUS ${OpenMP_CXX_LIBRARIES})
message(STATUS ${OpenMP_C_LIBRARIES})
set(CMAKE_VERBOSE_MAKEFILE ON)


include_directories(/usr/local/include)
include_directories(/usr/include)
include_directories(SYSTEM ${MPI_INCLUDE_PATH})
include_directories(SYSTEM ${OpenMP_INCLUDE_PATH})
target_link_libraries(${PROJECT_NAME} ${MPI_CXX_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${OpenMP_CXX_LIBRARIES})