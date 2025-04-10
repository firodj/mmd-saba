cmake_minimum_required (VERSION 2.8)

project (SoLoud)

set (CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake;${CMAKE_MODULE_PATH}")
set (CMAKE_POSITION_INDEPENDENT_CODE ON)
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../bin" )
#INCLUDE (StandartIncludes)

include_directories ("${CMAKE_CURRENT_SOURCE_DIR}/../include")

include (Configure.cmake)
#INCLUDE (InstallIncludes.cmake)
#INCLUDE (InstallStaticData.cmake)

if (UNIX AND NOT WIN32 AND NOT APPLE)
	if (CMAKE_SIZEOF_VOID_P MATCHES "8")
		set (LIB_POSTFIX "64" CACHE STRING "suffix for 32/64 dir placement")
		mark_as_advanced (LIB_POSTFIX)
	endif ()
endif ()
if (NOT DEFINED LIB_POSTFIX)
	set (LIB_POSTFIX "")
endif ()

include (src.cmake)

# Demos
IF (SOLOUD_BUILD_DEMOS)
	include (demos.cmake)
endif ()

include (InstallExport)
