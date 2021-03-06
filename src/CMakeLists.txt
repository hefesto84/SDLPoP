cmake_minimum_required(VERSION 2.8)
project(SDLPoP)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -std=gnu99")

if (WIN32)
    # Use the -mwindows compiler flag when compiling with MinGW to hide the console window
    # Only do this when not in debug mode
    if (NOT (CMAKE_BUILD_TYPE STREQUAL "Debug"))
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mwindows")
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mwindows")
    endif (NOT (CMAKE_BUILD_TYPE STREQUAL "Debug"))
endif(WIN32)

# have CMake output binaries to the directory that contains the source files
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${SDLPoP_SOURCE_DIR}/..")

# if SDL_2, SDL2_image and SDL2_mixer are not in the toolchain/build environment, specify /include and /lib paths:

#set(DIR_SDL2 "C:/SDL2-2.0.3")
#include_directories(${DIR_SDL2}/include)
#link_directories(${DIR_SDL2}/lib)

set(SOURCE_FILES
        main.c
        common.h
        config.h
        data.c
        data.h
        proto.h
        seg000.c
        seg001.c
        seg002.c
        seg003.c
        seg004.c
        seg005.c
        seg006.c
        seg007.c
        seg008.c
        seg009.c
        seqtbl.c
        options.c
        replay.c
        types.h
        icon.rc
        lighting.c
        screenshot.c
        )
add_executable(prince ${SOURCE_FILES})

if(WIN32)
    target_link_libraries(prince mingw32 SDL2main SDL2 SDL2.dll SDL2_image SDL2_mixer)
else()
    target_link_libraries(prince SDL2main SDL2 SDL2_image SDL2_mixer m)
endif()

