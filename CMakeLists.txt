cmake_minimum_required(VERSION 3.14)
project(obscura_proto_native LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

option(BUILD_TESTING "Build tests" OFF)

include(FetchContent)

FetchContent_Declare(
    ObscuraProto
    GIT_REPOSITORY https://github.com/ObscuraEcosystem/ObscuraProto.git
    GIT_TAG        v1.0.1
)
FetchContent_MakeAvailable(ObscuraProto)
