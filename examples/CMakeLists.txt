include_directories( ../lib )
add_executable( example example.cpp )
target_link_libraries( example gop_imgproc gop_proposals gop_contour )

add_executable( example_learned example_learned.cpp )
target_link_libraries( example_learned gop_imgproc gop_proposals gop_contour )
