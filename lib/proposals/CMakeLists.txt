add_library( gop_proposals saliency.cpp objectives.cpp unaryfeature.cpp unary.cpp edgefeature.cpp proposal.cpp geodesics.cpp seedfeature.cpp seed.cpp edgeweight.cpp )
target_link_libraries( gop_proposals gop_util gop_learning gop_imgproc gop_contour lbfgs gop_segmentation )
