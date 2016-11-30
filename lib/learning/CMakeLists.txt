add_library( gop_learning splitcriterion.cpp treedata.cpp tree.cpp forest.cpp features.cpp )
target_link_libraries( gop_learning gop_util )
