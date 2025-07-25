cmake_minimum_required(VERSION 3.10)
SET(CMAKE_CXX_STANDARD 17)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

######################## EDIT IF REQUIRED ####################
# ###Uncomment the line below and specify the path to OpenCV directory i.e. the path to the OpenCVConfig.cmake file. Check the examples given below.
#SET(OpenCV_DIR Enter-the-path-of-OpenCV-installation-on-your-system)


################### OpenCV_DIR Examples  #####################

### MACOS : /usr/local/Cellar/opencv/3.3.1_1/share/OpenCV/

### UBUNTU : /usr/local/share/OpenCV/

### WINDOWS : C:\Users\yourname\Documents\opencv-3.3.1\build\install

##############################################################




###################   ***DO NOT EDIT***  #####################

#############  Common Instructions for all Users  ############
if(MSVC)
SET(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
endif()

#chroma_key
project(chroma_key)
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS})



# 1. Executable
add_executable(chroma_key
  ${CMAKE_SOURCE_DIR}/src/chroma_key.cpp
)

# 2
configure_file(
  ${CMAKE_SOURCE_DIR}/src/config.pch.in
  ${CMAKE_SOURCE_DIR}/src/config.pch
  @ONLY
)

# 3. Headers and libs
#target_include_directories(chroma_key PRIVATE include)
target_link_libraries(chroma_key PRIVATE ${OpenCV_LIBS})

# 4. Reference needed data
target_compile_definitions(chroma_key PRIVATE
  DATA_DIR=\"${CMAKE_SOURCE_DIR}/data\"
)