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

set(ADDITIONAL_LIBRARIES "")

option(OPENNI2_ORBBEC_SOFTFILTER "Use software filter for depth data" ON)

if(OPENNI2_ORBBEC_SOFTFILTER)
	add_definitions(-DFILTER=1)
	
	SET(FILTER_ROOT "${PROJECT_SOURCE_DIR}/ThirdParty/Orbbec/filter")
	IF(${CMAKE_SYSTEM_PROCESSOR} MATCHES "aarch64")
		SET(FILTER_LIB "${FILTER_ROOT}/Arm64-Release/libSoftFilter.a")
	elseif(${CMAKE_SYSTEM_PROCESSOR} MATCHES "arm")
		SET(FILTER_LIB "${FILTER_ROOT}/Arm-Release/libSoftFilter.a")
	else()
		SET(FILTER_LIB "${FILTER_ROOT}/x86-Release/libSoftFilter.a")
	endif()
	message(STATUS "Adding software filter from ${FILTER_LIB}")
	LIST(APPEND ADDITIONAL_LIBRARIES ${FILTER_LIB})
endif(OPENNI2_ORBBEC_SOFTFILTER)

set(openni2_orbbec_SRC ${openni2_orbbec_SRC} ${depth_utils_SRC})
add_library(orbbec SHARED ${openni2_orbbec_SRC})
target_link_libraries(orbbec ${XnLib_LIBS} xnlib ${ADDITIONAL_LIBRARIES})
install(TARGETS orbbec LIBRARY DESTINATION lib/OpenNI2/Drivers ARCHIVE DESTINATION lib)