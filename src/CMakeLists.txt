INCLUDE_DIRECTORIES(.)
FILE(GLOB hdrs "*.h*")
FILE(GLOB srcs "*.c*")


SET(hdrs ${hdrs})
SET(srcs ${srcs})


ADD_LIBRARY(${PROJECT_NAME} ${srcs} ${hdrs})
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR} )
INCLUDE_DIRECTORIES(${GNULIBS_INCLUDE_DIR})
include_directories ("/usr/share/OGRE/Samples/Common/include/") 
include_directories (${OGRE_INCLUDE_DIRS})
include_directories (${OIS_INCLUDE_DIRS})
include_directories (${aruco_INCLUDE_DIRS})
MESSAGE(STATUS "OpenCV_LIB_DIR=${OpenCV_LIB_DIR}")
# SET_TARGET_PROPERTIES(${PROJECT_NAME} PROPERTIES
#	DEFINE_SYMBOL DSO_EXPORTS
#	VERSION ${PROJECT_VERSION}
#	SOVERSION ${PROJECT_SOVERSION}
#	CLEAN_DIRECT_OUTPUT 1 					# allow creating static and shared libs without conflicts
#	OUTPUT_NAME "${PROJECT_NAME}${PROJECT_DLLVERSION}" 	# avoid conflicts between library and binary target names
#)

TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${REQUIRED_LIBRARIES})

INSTALL(TARGETS ${PROJECT_NAME}
	RUNTIME DESTINATION bin COMPONENT main			# Install the dll file in bin directory
	LIBRARY DESTINATION lib PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE COMPONENT main
	ARCHIVE DESTINATION lib COMPONENT main)			# Install the dll.a file in lib directory

INSTALL(FILES ${hdrs}
	DESTINATION include/${PROJECT_NAME}
	COMPONENT main)

