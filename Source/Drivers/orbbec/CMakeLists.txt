# Build OpenNI Orbbec Drivers

include_directories(".")
include_directories("Include")
file(GLOB openni2_orbbec_SRC
  "Core/*.cpp"
  "DDK/*.cpp"
  "DriverImpl/*.cpp"
  "Formats/*.cpp"
  "Sensor/*.cpp"
)

set(openni2_orbbec_SRC ${openni2_orbbec_SRC} ${depth_utils_SRC})
add_library(orbbec SHARED ${openni2_orbbec_SRC})
target_link_libraries(orbbec ${XnLib_LIBS} xnlib)
install(TARGETS orbbec LIBRARY DESTINATION lib/OpenNI2/Drivers ARCHIVE DESTINATION lib)