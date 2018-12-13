cmake_minimum_required(VERSION 3.4 FATAL_ERROR)

project(libuiohook)

add_library(
	uiohook
	src/logger.c src/logger.h
)

if(UNIX)
	find_package(X11 REQUIRED)

	target_sources(
		uiohook PRIVATE
		src/x11/input_helper.c
		src/x11/input_helper.h
		src/x11/input_hook.c
		src/x11/post_event.c
		src/x11/system_properties.c
	)

endif()

if(WIN32)
	target_sources(
		uiohook PRIVATE
		src/windows/input_helper.c
		src/windows/input_helper.h
		src/windows/input_hook.c
		src/windows/post_event.c
		src/windows/system_properties.c
	)
endif()

if(APPLE)
	target_sources(
		uiohook PRIVATE
		src/darwin/input_helper.c
		src/darwin/input_helper.h
		src/darwin/input_hook.c
		src/darwin/post_event.c
		src/darwin/system_properties.c
	)
endif()

target_include_directories(
	uiohook
	PUBLIC include/
	PRIVATE src/
)