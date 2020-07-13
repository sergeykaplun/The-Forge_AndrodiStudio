cmake_minimum_required(VERSION 3.4.1)
set(NAME 04_ExecuteIndirect)
add_definitions(-DVK_USE_PLATFORM_ANDROID_KHR
                -DGAINPUT_PLATFORM_ANDROID
                -DANDROID_ARM_NEON
                -DANDROID
                -DVULKAN)

add_subdirectory(../TheForgeBase ${CMAKE_SOURCE_DIR}/../TheForgeBase)

set(FORGE_ROOT ../../../The-Forge/)
set(UT_ROOT ${FORGE_ROOT}Examples_3/Unit_Tests/src)

add_library(native_app_glue STATIC
        ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c)
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")

include_directories(${ANDROID_NDK}/sources/android/native_app_glue)
file(GLOB UT_SRC ${UT_ROOT}/${NAME}/*.cpp)
add_library(${NAME} SHARED ${UT_SRC})
target_link_libraries( ${NAME}
                       native_app_glue
                       theforgebase
                       log
                       android
                       )