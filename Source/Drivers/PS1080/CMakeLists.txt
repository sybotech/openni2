# Build OpenNI PS1080 Drivers
include_directories("Include")
include_directories(".")

file(GLOB openni2_ps1080_SRC
  "Core/*.cpp"
  "DDK/*.cpp"
  "DriverImpl/*.cpp"
  "Formats/*.cpp"
  "Sensor/*.cpp"
)

set(openni2_ps1080_SRC ${openni2_ps1080_SRC} ${depth_utils_SRC})
add_library(PS1080 SHARED ${openni2_ps1080_SRC})
target_link_libraries(PS1080 ${XnLib_LIBS} xnlib)
install(TARGETS PS1080 LIBRARY DESTINATION lib/OpenNI2/Drivers ARCHIVE DESTINATION lib)