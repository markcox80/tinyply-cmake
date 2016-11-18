set(P_PROJECT_NAME tinyply)
project(${P_PROJECT_NAME})

cmake_minimum_required(VERSION 3.4.2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(P_INSTALL_PREFIX ${CMAKE_INSTALL_PREFIX})
set(P_HEADER_PREFIX ${P_INSTALL_PREFIX}/include)
set(P_LIB_PREFIX ${P_INSTALL_PREFIX}/lib)
set(P_EXPORTS_PREFIX ${P_INSTALL_PREFIX}/share/tinyply)

add_library(tinyply tinyply/source/tinyply.cpp)
target_include_directories(tinyply PUBLIC $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/tinply/source/>
                                          $<INSTALL_INTERFACE:${P_HEADER_PREFIX}>)

set_target_properties(tinyply PROPERTIES INSTALL_NAME_DIR ${P_LIB_PREFIX})

install(EXPORT tinyply
        DESTINATION ${P_EXPORTS_PREFIX})

install(TARGETS tinyply
        EXPORT tinyply
        ARCHIVE DESTINATION ${P_LIB_PREFIX}
        LIBRARY DESTINATION ${P_LIB_PREFIX})

install(FILES tinyply/source/tinyply.h
        DESTINATION ${P_HEADER_PREFIX})

configure_file(config.cmake.in tinyply-config.cmake)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/tinyply-config.cmake
        DESTINATION ${P_EXPORTS_PREFIX})

add_custom_target(tests
                  COMMAND echo "No tinyply tests."
                  DEPENDS tinyply)
