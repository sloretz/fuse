find_package(fuse_constraints REQUIRED)
find_package(fuse_graphs REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)

# CORE GTESTS ======================================================================================
ament_add_gtest("test_stamped_variable_synchronizer" "test_stamped_variable_synchronizer.cpp")
target_link_libraries("test_stamped_variable_synchronizer"
  ${PROJECT_NAME}
  fuse_constraints::fuse_constraints
  fuse_graphs::fuse_graphs
)


# ROS TESTS (WITH LAUNCH) ==========================================================================
find_package(ament_cmake_pytest REQUIRED)

ament_add_gtest_executable(test_path_2d_publisher launch_tests/test_path_2d_publisher.cpp)
target_link_libraries(test_path_2d_publisher
  ${PROJECT_NAME}
  fuse_constraints::fuse_constraints
  fuse_graphs::fuse_graphs
  tf2::tf2
  ${geometry_msgs_TARGETS}
  ${nav_msgs_TARGETS}
  ${tf2_geometry_msgs_TARGETS}
)
ament_add_pytest_test(test_path_2d_publisher_py "launch_tests/test_path_2d_publisher.py"
  WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
)

# ament_add_gtest_executable(test_pose_2d_publisher launch_tests/test_pose_2d_publisher.cpp)
# target_link_libraries(test_pose_2d_publisher
#   ${PROJECT_NAME}
#   fuse_constraints::fuse_constraints
#   fuse_graphs::fuse_graphs
# )
# ament_add_pytest_test(test_pose_2d_publisher_py "launch_tests/test_pose_2d_publisher.py"
#   WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
# )

configure_file("launch_tests/test_path_2d_publisher.yaml" "launch_tests/test_path_2d_publisher.yaml" COPYONLY)
configure_file("launch_tests/test_pose_2d_publisher.yaml" "launch_tests/test_path_2d_publisher.yaml" COPYONLY)
