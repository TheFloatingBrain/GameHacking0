cmake_minimum_required(VERSION 3.5)
project(Demo)
set(CMAKE_CXX_STANDARD 23)
#
include(FetchContent)

#find_package(xtensor)# CONFIG REQUIRED)
FetchContent_Declare(
	raylib
	GIT_REPOSITORY "https://github.com/raysan5/raylib.git"
	GIT_TAG "master"
	GIT_PROGRESS TRUE
)

message("Fetched Raylib")
FetchContent_Declare(
	bullet3
	GIT_REPOSITORY "https://github.com/physics-playground/Bullet.git"
	GIT_TAG "main"
	GIT_PROGRESS TRUE
)
message("Fetched Bullet3 Physics Engine")
#
FetchContent_MakeAvailable(raylib)
message("Raylib Made Availible")
set(BUILD_CPU_EXAMPLES OFF)
set(BUILD_UNIT_TESTS OFF)
FetchContent_MakeAvailable(bullet3)
message("Bullet3 Physics Engine Made Availible")
include_directories(${bullet3_SOURCE_DIR}/src) # (1)
message("Bullet3 Physics Engine Include Directory Made Availible")
#add_subdirectory(${bullet3_SOURCE_DIR}/bullet3) # (2)

file(GLOB_RECURSE SOURCES "Source/*.cpp")
add_executable(demo ${SOURCES})# "include/Ray/rlight.h")
target_link_libraries(demo PRIVATE raylib BulletDynamics BulletCollision LinearMath)
# target_link_libraries(BlockBuilder PRIVATE xtensor)
target_include_directories(demo PRIVATE Include)
#file(COPY "resources/" DESTINATION "resources/")

