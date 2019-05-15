cmake_minimum_required(VERSION 3.13)
set(LibName utils_simple_logmanager)
project(${LibName})

include(FetchContent)
FetchContent_Declare( al2o3 GIT_REPOSITORY https://github.com/DeanoC/al2o3 GIT_TAG master )
FetchContent_GetProperties(al2o3)
if(NOT al2o3_POPULATED)
	FetchContent_Populate(al2o3)
	add_subdirectory(${al2o3_SOURCE_DIR} ${al2o3_BINARY_DIR})
endif()

set(Interface
		logmanager.h
		)
set(Src
		logmanager.c
		)

set(Deps
		al2o3_platform
		al2o3_os
		)

ADD_LIB(${LibName} "${Interface}" "${Src}" "${Deps}")

set( Tests
		runner.cpp
		test_logmanager.cpp
		)
set( TestDeps
		al2o3_catch2 )
ADD_LIB_TESTS(${LibName} "${Interface}" "${Tests}" "${TestDeps}")