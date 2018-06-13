#----------------------------------------------------------------------------

# Setup the project

#

cmake_minimum_required(VERSION 2.6 FATAL_ERROR)

project(simLab)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(CMAKE_BUILD_TYPE Debug)

set(useROOT true)        # use true or false

include(FindROOT.cmake)
	include_directories(${PROJECT_SOURCE_DIR} ${ROOT_INCLUDE_DIR} )

	set(LINK_DIRECTORIES

	  ${ROOT_LIBRARY_DIR}	

	  )

	file(GLOB sources 
	  ${PROJECT_SOURCE_DIR}/simLab.cc
	  ${PROJECT_SOURCE_DIR}/TLab.C
	  ${PROJECT_SOURCE_DIR}/TSim.C
	  ${PROJECT_SOURCE_DIR}/TTheory.C


	  )

	file(GLOB headers 
	  ${PROJECT_SOURCE_DIR}/includes.h
	  ${PROJECT_SOURCE_DIR}/TLab.h
	  ${PROJECT_SOURCE_DIR}/TSim.h
	  ${PROJECT_SOURCE_DIR}/TTheory.h

	  )

link_directories( ${LINK_DIRECTORIES})

#----------------------------------------------------------------------------

# Add the executable, and link it to the Geant4 libraries

#

add_executable(simLab ${sources} ${headers})


	set(LINK_LIBRARIES

  ${ROOT_LIBRARIES} -lThread -lGed -lEG -lGeom 

)


target_link_libraries(simLab ${LINK_LIBRARIES})




#----------------------------------------------------------------------------

# Install the executable to 'bin' directory under CMAKE_INSTALL_PREFIX

#

install(TARGETS simLab DESTINATION bin)
