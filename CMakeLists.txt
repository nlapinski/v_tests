cmake_minimum_required(VERSION 3.2)
project(v_test)

set(SOURCE_FILES
  main.c
)


add_executable(v_test ${SOURCE_FILES})

#Sets a base path for the includes so that they can be used in the same way as in Visual Studio/Codeblocks
set(BASEPATH "${CMAKE_SOURCE_DIR}/src")
include_directories("${BASEPATH}")

#Setting up PkgConfig
find_package(PkgConfig REQUIRED)

#Finding and linking GLFW3
pkg_search_module(GLFW3 3.2 REQUIRED glfw3)
if(GLFW3_FOUND)
    message(STATUS "Found GLFW, Including and Linking now")
    include_directories(${GLFW3_INCLUDE_DIRS})
    target_link_libraries(v_test ${GLFW3_STATIC_LIBRARIES})
endif(GLFW3_FOUND)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

#Finding and linking Vulkan
find_package (Vulkan REQUIRED)
if (Vulkan_FOUND)
    message(STATUS "Found Vulkan, Including and Linking now")
    include_directories(${Vulkan_INCLUDE_DIRS})
    target_link_libraries (v_test ${Vulkan_LIBRARIES})
    message(STATUS "Vulkan Include dirs: ${Vulkan_INCLUDE_DIRS} and libs: ${Vulkan_LIBRARIES}")
endif (Vulkan_FOUND)

#Finding and linking ASSIMP



find_package(ASSIMP REQUIRED)
if(ASSIMP_FOUND)
    message(STATUS "Found ASSIMP, Including and Linking now")
    include_directories(${ASSIMP_INCLUDE_DIR})
    target_link_libraries (v_test ${ASSIMP_LIBRARY})
    #message(STATUS ${ASSIMP_INCLUDE_DIR})
endif (ASSIMP_FOUND)