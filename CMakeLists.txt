cmake_minimum_required(VERSION 3.4.1)

project(airplay-server)

set (CMAKE_CXX_STANDARD 11)

set (RENDERER_FLAGS "")

add_subdirectory(lib/curve25519)
add_subdirectory(lib/ed25519)
add_subdirectory(lib/playfair)
add_subdirectory(lib/llhttp)
add_subdirectory(lib)
add_subdirectory(renderers)

# Make sure the main executable is aware of the available renderers
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${RENDERER_FLAGS}" )

add_executable( airplay-server airplay-server.cpp)
target_link_libraries ( airplay-server renderers airplay )

install(PROGRAMS airplay-server DESTINATION bin)
