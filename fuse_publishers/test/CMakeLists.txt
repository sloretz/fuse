find_package(fuse_constraints)
find_package(fuse_graphs)

# CORE GTESTS ======================================================================================
set(TEST_TARGETS
  test_path_2d_publisher
  test_pose_2d_publisher
  test_stamped_variable_synchronizer
)

foreach(test_name ${TEST_TARGETS})
  ament_add_gtest("${test_name}" "${test_name}.cpp")
  target_link_libraries("${test_name}"
    ${PROJECT_NAME}
    fuse_constraints::fuse_constraints
    fuse_graphs::fuse_graphs
  )
endforeach()
