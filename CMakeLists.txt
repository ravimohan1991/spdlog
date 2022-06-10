# Copyright(c) 2019 spdlog authors Distributed under the MIT License (http://opensource.org/licenses/MIT)

set(SPDLOG_SRCS src/dummy.cpp)
#file(GLOB_RECURSE HEADERFILES ${CMAKE_CURRENT_SOURCE_DIR}/include/spdlog/*.h)

# Some preprocessor definitions
add_compile_definitions(SPDLOG_COMPILED_LIB)

# Since Windows has exception with regards to Static/Dynamic libraries, we just compile a dummy
if (BUILD_SHARED_LIBS)
    add_library(spdlogging SHARED ${SPDLOG_SRCS} ${HEADERFILES})
else()
    add_library(spdlogging STATIC ${SPDLOG_SRCS} ${HEADERFILES})
endif()

target_include_directories(spdlogging
    PRIVATE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>")

target_compile_definitions(spdlogging PUBLIC spdlogging)

