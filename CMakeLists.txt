if(NOT ENABLE_GUI)
  return()
endif()

option(BUILD_RTF_TEST_PLANT "Building the RTF test plant models" OFF)
if(NOT BUILD_RTF_TEST_PLANT)
  return()
endif()

if(NOT DEFINED ENV{ROS_DISTRO})
  if(UNIX)
    add_custom_target(
      symlink_to_RTF_TEST_PLANT ALL
      COMMAND ${CMAKE_COMMAND} -E create_symlink
      ${CMAKE_CURRENT_SOURCE_DIR} ${CNOID_BINARY_SHARE_DIR}/RTF-TestPlant)
  endif()

  install(DIRECTORY
    model
    project
    script
    DESTINATION ${CNOID_SHARE_SUBDIR}/RTF-TestPlant)
else()
  cmake_minimum_required(VERSION 3.5.0)
  project(rtf-test-plant)
  
  find_package(catkin REQUIRED COMPONENTS
    choreonoid
    )

  install(DIRECTORY
    model
    project
    script
    DESTINATION ${CHOREONOID_SHARE_SUBDIR}/RTF-TestPlant)
endif()
