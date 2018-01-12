# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.
set(OPENCV_DIR /Users/jdwish/Library/Android/OpenCV-android-sdk/sdk)

cmake_minimum_required(VERSION 3.4.1)

add_library( # Sets the name of the library.
             native-lib

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/DetectionBasedTracker_jni.cpp )

#添加下载的OpenCV-android-sdk路径
include_directories(${OPENCV_DIR}/native/jni/include)
add_library( lib-opencv SHARED IMPORTED )
#项目需要添加jniLibs
set_target_properties(lib-opencv PROPERTIES IMPORTED_LOCATION  ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )


target_link_libraries( # Specifies the target library.
                       native-lib
                       lib-opencv
                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )