add_library( gop_segmentation aggregation.cpp iouset.cpp segmentation.cpp )
target_link_libraries( gop_segmentation gop_util gop_learning gop_imgproc gop_contour )
