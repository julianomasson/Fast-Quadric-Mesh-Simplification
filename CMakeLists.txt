cmake_minimum_required(VERSION 3.14)
project(FastQuadricMeshSimplification)

# Allow the user to build a static library
option(BUILD_SHARED_LIBS "Build shared libraries (DLL)" ON)
set(CMAKE_DEBUG_POSTFIX "d")

add_library(${PROJECT_NAME}    	src/FastQuadricMeshSimplification.cpp
			       	src/FastQuadricMeshSimplification.h
			       	src/SymetricMatrix.cpp
			       	src/SymetricMatrix.h
			       	src/VecMath.cpp
				src/VecMath.h)

# Specific flags depending on platform
if(WIN32)
    add_definitions(-DNOMINMAX -DFOUG_OS_WINDOWS)
elseif(APPLE)
    add_definitions(-DFOUG_OS_MAC)
elseif(UNIX)
    add_definitions(-DFOUG_OS_UNIX)
endif()

if(BUILD_SHARED_LIBS)
    add_definitions(-DFASTQUADRICMESHSIMPLIFICATION_LIB_DLL
                    -DFASTQUADRICMESHSIMPLIFICATION_LIB_MAKE_DLL)
endif()

# Declare installs
install(FILES	src/FastQuadricMeshSimplification.h
		src/SymetricMatrix.h
		src/VecMath.h
        DESTINATION include)
install(TARGETS ${PROJECT_NAME}
          RUNTIME DESTINATION lib
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)

message(STATUS "CMAKE_CXX_FLAGS = ${CMAKE_CXX_FLAGS}")