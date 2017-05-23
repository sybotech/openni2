include_directories(DepthUtils)

file(GLOB depth_utils_SRC
  "./DepthUtils/*.cpp"
)

add_subdirectory("Drivers/PS1080")
add_subdirectory("Drivers/orbbec")