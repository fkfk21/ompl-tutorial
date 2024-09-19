cmake_minimum_required(VERSION 3.0)
project(ompl_tutorial CXX)

# OMPLのパスを指定する
set(OMPL_DIR "/opt/ros/humble/share/ompl/cmake")
find_package(ompl REQUIRED)
message(STATUS "Found OMPL version: ${ompl_VERSION}")

# ライブラリやヘッダーの設定を追加する
include_directories(${OMPL_INCLUDE_DIRS})

file(GLOB SRCS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} ./src/*.cpp)
foreach(file ${SRCS})
  string(REPLACE ".cpp" "" name ${file})
  file(RELATIVE_PATH name ${CMAKE_CURRENT_SOURCE_DIR}/src ${CMAKE_CURRENT_SOURCE_DIR}/${name})
  add_executable(${name} ${file})
  target_link_libraries(${name} ${OMPL_LIBRARIES})
endforeach(file ${SRCS})


