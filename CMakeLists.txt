cmake_minimum_required(VERSION 3.5)
project(motion-effect)

set(motion-transition_SOURCES
	./src/helper.c
	./src/motion-transition/motion-transition.c
)

set(motion-transition_HEADERS
	./src/helper.h
)

add_library(motion-transition MODULE)
add_library(OBS::mtransition ALIAS motion-transition)

target_sources(
	motion-transition
	PRIVATE ${motion-transition_SOURCES}
	${motion-transition_HEADERS})

target_link_libraries(motion-transition PRIVATE OBS::libobs)

set_target_properties(motion-transition PROPERTIES FOLDER "plugins/motion-transition")

set_property(GLOBAL APPEND PROPERTY OBS_MODULE_LIST "motion-transition")
set_target_properties(motion-transition PROPERTIES PREFIX "")

setup_plugin_target(motion-transition)