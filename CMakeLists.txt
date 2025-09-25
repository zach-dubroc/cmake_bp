# ZD CMAKE TEMPLATE 
cmake_minimum_required(VERSION 3.13)
project(main1)
set(CMAKE_CXX_STANDARD 17)


set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>")

# defining MY_SOURCES as a list of all project source files
file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
add_executable(main1 ${MY_SOURCES})

# optional sub_d
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/thirdParty/profilerLib/CMakeLists.txt")
    add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/thirdParty/profilerLib")
    target_link_libraries(main1 PRIVATE profilerLib)
endif()

if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/thirdParty/safeSave/CMakeLists.txt")
    add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/thirdParty/safeSave")
    target_link_libraries(main1 PRIVATE safeSave)
endif()


# before sending anywhere swap to relative path, use abs for dev
target_compile_definitions(main1 PUBLIC RESOURCES_PATH="${CMAKE_CURRENT_SOURCE_DIR}/resources")
# target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC RESOURCES_PATH="${CMAKE_CURRENT_SOURCE_DIR}/resources")
# target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC RESOURCES_PATH="/resources")

target_include_directories(main1 PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_link_libraries(main1 PRIVATE profilerLib)


find_package(fmt CONFIG REQUIRED)
target_link_libraries(main PRIVATE fmt::fmt)

# Or use the header-only version
find_package(fmt CONFIG REQUIRED)
target_link_libraries(main1 PRIVATE fmt::fmt-header-only)
