# Find Python and boost python
# if(USE_PYTHON EQUAL 2)
	find_package(PythonInterp 2.7 REQUIRED)
	find_package(PythonLibs 2.7 REQUIRED)
	find_package(NumPy REQUIRED)
	find_package(Boost COMPONENTS python REQUIRED)
# else()
# 	find_package(PythonInterp 3.3 REQUIRED)
# 	find_package(PythonLibs 3.3 REQUIRED)
# 	find_package(NumPy REQUIRED)
# 	find_package(Boost COMPONENTS python-py34)
# 	if(NOT Boost_FOUND)
# 		find_package(Boost COMPONENTS python-py33)
# 	endif()
# 	if(NOT Boost_FOUND)
# 		find_package(Boost COMPONENTS python3 REQUIRED)
# 	endif()
# endif()

include_directories( ${Boost_INCLUDE_DIRS} ${PYTHON_INCLUDE_DIRS} ${PROJECT_SOURCE_DIR}/external/Boost.NumPy ${NUMPY_INCLUDE_DIRS} ${PYTHON_INCLUDE_DIRS} )
link_directories( ${Boost_LIBRARY_DIR} )

# Find zlib to load the datasets
find_package( ZLIB )
set(DATASET_SRC "" )
set(DATASET_LIB "" )
if( ZLIB_FOUND )
	set(DATASET_SRC dataset.cpp )
	set(DATASET_LIB gop_dataset )
	add_subdirectory(dataset)
	add_definitions(-DUSE_DATASET)
endif()

file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/__init__.py" "" )

if( UNIX )
	# Disable the pointer-to-function and pointer-to-object warnings
	set_property(SOURCE util.cpp PROPERTY COMPILE_FLAGS -w )
endif()

add_library( gop SHARED gop.cpp boost.cpp util.cpp map.cpp contour.cpp ${DATASET_SRC} imgproc.cpp learning.cpp segmentation.cpp proposals.cpp )
target_link_libraries( gop gop_util ${Boost_LIBRARIES} ${PYTHON_LIBRARIES} boost_numpy ${DATASET_LIB} gop_imgproc gop_learning gop_contour gop_segmentation gop_proposals )
set_target_properties( gop PROPERTIES PREFIX "")
if(APPLE)
	set_target_properties( gop PROPERTIES SUFFIX ".so" )
endif()

INSTALL(TARGETS gop DESTINATION ${CMAKE_INSTALL_PREFIX}/lib )
