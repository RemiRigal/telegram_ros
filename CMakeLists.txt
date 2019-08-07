cmake_minimum_required(VERSION 2.8.3)
project(telegram_ros)

find_package(catkin REQUIRED)

catkin_package()

catkin_install_python(PROGRAMS
  scripts/telegram_ros_bridge
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/scripts
)


install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)
