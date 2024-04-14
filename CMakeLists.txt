cmake_minimum_required(VERSION 3.5)
project(AKFSFSimulation CXX)

set(CMAKE_CXX_STANDARD 17)

# Set the path to Eigen3 include directory
set(EIGEN3_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/eigen3)

# Set the path to SDL2 include directory
set(SDL2_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/SDL2-2.30.2/include)

# Set the path to SDL2_ttf include directory
set(SDL2_TTF_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/SDL2_ttf-2.22.0/include)

# Set the path to SDL2 library directory
set(SDL2_LIBRARY_DIR "C:/Users/aha/Desktop/AI_Team/Kalman_Filter/SDL2-2.30.2/lib/x64")


# Set the path to SDL2_ttf library directory
set(SDL2_TTF_LIBRARY_DIR "C:/Users/aha/Desktop/AI_Team/Kalman_Filter/SDL2_ttf-2.22.0/lib/x64")


# Source files
set(SRC_CPP
    src/main.cpp
    src/display.cpp
    src/beacons.cpp
    src/sensors.cpp
    src/simulation.cpp
    src/utils.cpp
    src/kalmanfilter.cpp
)

# Add executable target
add_executable(AKFSFSimulation ${SRC_CPP})

# Include directories
target_include_directories(AKFSFSimulation PUBLIC
    ${EIGEN3_INCLUDE_DIR}
    ${SDL2_INCLUDE_DIR}
    ${SDL2_TTF_INCLUDE_DIR}
)

# Link libraries
target_link_libraries(AKFSFSimulation PUBLIC
    ${SDL2_LIBRARY_DIR}/SDL2.lib
    ${SDL2_TTF_LIBRARY_DIR}/SDL2_ttf.lib
)

# Copy DLLs to the output directory
add_custom_command(TARGET AKFSFSimulation POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        ${SDL2_LIBRARY_DIR}/SDL2.dll
        ${SDL2_TTF_LIBRARY_DIR}/SDL2_ttf.dll
        $<TARGET_FILE_DIR:AKFSFSimulation>
)
