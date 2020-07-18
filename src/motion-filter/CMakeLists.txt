cmake_minimum_required(VERSION 3.5)
project(motion-filter)

set(motion-filter_SOURCES
	../helper.c
	motion-filter.c
	)
	
set(motion-filter_HEADERS
	../helper.h
	)	
	
add_library(motion-filter MODULE
	${motion-filter_SOURCES}
	${motion-filter_HEADERS})
	
target_link_libraries(motion-filter
	libobs)

if(UNIX AND NOT APPLE)

	if(ARCH EQUAL 64)
		set(ARCH_NAME "x86_64")
	else()
		set(ARCH_NAME "i686")
	endif()

	set_target_properties(motion-filter PROPERTIES PREFIX "")

	install(TARGETS motion-filter
		LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/obs-plugins)
	install(DIRECTORY ${CMAKE_SOURCE_DIR}/data/motion-filter/
		DESTINATION "${CMAKE_INSTALL_PREFIX}/share/obs/obs-plugins/motion-filter/")
endif()

#install_obs_plugin(motion-filter) 
