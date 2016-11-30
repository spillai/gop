add_library( gop_contour directedsobel.cpp boundarydetector.cpp sketchtokens.cpp structuredforest.cpp )
target_link_libraries( gop_contour gop_util gop_imgproc gop_learning )
