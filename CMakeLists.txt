CMAKE_MINIMUM_REQUIRED(VERSION 2.4)
PROJECT(BIGRCarotid)

if(COMMAND cmake_policy)
  cmake_policy(SET CMP0003 NEW)
  cmake_policy(SET CMP0015 NEW)
endif(COMMAND cmake_policy)

IF(MSVC)
  SET (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")
  SET (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /bigobj")
  # This disables the warning on std::copy unsafe parameters in itk headers.
  SET (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /wd4996")
ENDIF(MSVC)

SET(Boost_USE_STATIC_LIBS   ON)
SET(Boost_USE_MULTITHREADED ON)
FIND_PACKAGE(Boost REQUIRED COMPONENTS filesystem program_options)
#FIND_PACKAGE(Boost)
IF(Boost_FOUND)
  INCLUDE_DIRECTORIES( ${Boost_INCLUDE_DIRS})
	LINK_DIRECTORIES( ${Boost_LIBRARY_DIRS})
ELSE(Boost_FOUND)
  MESSAGE(FATAL_ERROR
          "Cannot build without boost. Please set BOOST_DIR.")
ENDIF(Boost_FOUND)


FIND_PACKAGE(ITK )
IF(ITK_FOUND)
  INCLUDE(${ITK_USE_FILE})
ELSE(ITK_FOUND)
  MESSAGE(FATAL_ERROR
          "Cannot build InsightApplications without ITK.  Please set ITK_DIR.")
ENDIF(ITK_FOUND)
IF(UNIX)
  LINK_LIBRARIES( 
    boost_filesystem
    boost_program_options
  )
ENDIF(UNIX)

SUBDIRS(
  
  medialness
  
)

