add_library( gop_util factory.cpp algorithm.cpp util.cpp eigen.cpp graph.cpp threading.cpp sse_defs.cpp optimization.cpp qp.cpp rasterize.cpp )
target_link_libraries( gop_util lbfgs )
