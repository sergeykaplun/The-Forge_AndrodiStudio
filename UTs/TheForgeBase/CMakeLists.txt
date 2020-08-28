cmake_minimum_required(VERSION 3.4.1)
set(FORGE_ROOT ../../../The-Forge/)

add_definitions("-DVK_USE_PLATFORM_ANDROID_KHR"
                "-DANDROID_ARM_NEON"
                "-DANDROID"
                "-DVULKAN"
                "-DDEBUG")

#add_subdirectory(${FORGE_ROOT}Common_3/ThirdParty/OpenSource/ozz-animation/src ${CMAKE_SOURCE_DIR}/build)

file(GLOB RENDER_COMMON_SRC ${FORGE_ROOT}Common_3/Renderer/*.cpp)
file(GLOB RENDER_VULKAN_SRC ${FORGE_ROOT}Common_3/Renderer/Vulkan/*.cpp)
file(GLOB OS_ANDROID_SRC ${FORGE_ROOT}Common_3/OS/Android/*.cpp)
file(GLOB OS_CAMERA_SRC ${FORGE_ROOT}Common_3/OS/Camera/*.cpp)
file(GLOB OS_CORE_SRC ${FORGE_ROOT}Common_3/OS/Core/*.cpp)
file(GLOB OS_FS_SRC ${FORGE_ROOT}Common_3/OS/FileSystem/*.cpp)
#file(GLOB OS_IMAGE_SRC ${FORGE_ROOT}Common_3/OS/Image/*.cpp)
file(GLOB OS_INPUT_SRC ${FORGE_ROOT}Common_3/OS/Input/*.cpp)
file(GLOB OS_LOGGING_SRC ${FORGE_ROOT}Common_3/OS/Logging/*.cpp)
file(GLOB OS_MEMTRACK_SRC ${FORGE_ROOT}Common_3/OS/MemoryTracking/*.cpp)
file(GLOB OS_PROFILER_SRC ${FORGE_ROOT}Common_3/OS/Profiler/*.cpp)
file(GLOB MIDDLEWARE_ANIMATION_SRC ${FORGE_ROOT}Middleware_3/Animation/*.cpp)
file(GLOB MIDDLEWARE_ECS_SRC ${FORGE_ROOT}Middleware_3/ECS/*.cpp)
file(GLOB MIDDLEWARE_TEXT_SRC ${FORGE_ROOT}Middleware_3/Text/*.cpp)
file(GLOB MIDDLEWARE_PANINI_SRC ${FORGE_ROOT}Middleware_3/PaniniProjection/*.cpp)
#file(GLOB MIDDLEWARE_UI_SRC ${FORGE_ROOT}/Middleware_3/UI/*.cpp)
set(MIDDLEWARE_UI_SRC "${FORGE_ROOT}Middleware_3/UI/AppUI.cpp;${FORGE_ROOT}Middleware_3/UI/ImguiGUIDriver.cpp")
#file(GLOB IMGUI_SRC ${FORGE_ROOT}/Common_3/ThirdParty/OpenSource/imgui/*.cpp)
set(IMGUI_SRC "${FORGE_ROOT}Common_3/ThirdParty/OpenSource/imgui/imgui.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/imgui/imgui_demo.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/imgui/imgui_draw.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/imgui/imgui_widgets.cpp")
file(GLOB BASISU_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/basis_universal/transcoder/*.cpp)
#file(GLOB EASTL_SRC ${FORGE_ROOT}/Common_3/ThirdParty/OpenSource/EASTL/*.cpp)
set(EASTL_SRC "${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/allocator_forge.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/assert.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/fixed_pool.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/hashtable.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/intrusive_list.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/numeric_limits.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/red_black_tree.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/string.cpp;${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/thread_support.cpp;")
file(GLOB EASTDC_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/EASTL/EAStdC/*.cpp)
file(GLOB ZIP_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/zip/*.cpp)
file(GLOB SPIRV_CROSS_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/SPIRV_cross/*.cpp)
file(GLOB SPIRV_TOOLS_SRC ${FORGE_ROOT}Common_3/Tools/SpirvTools/*.cpp)
file(GLOB GAINPUT_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/source/gainput/*.cpp)
file(GLOB GAINPUT_KBD_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/source/gainput/keyboard/*.*)
file(GLOB GAINPUT_PAD_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/source/gainput/pad/*.cpp)
file(GLOB GAINPUT_MOUSE_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/source/gainput/mouse/*.cpp)
file(GLOB GAINPUT_TOUCH_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/source/gainput/touch/*.cpp)
file(GLOB ANIMATION_SRC ${FORGE_ROOT}Middleware_3/Animation/*.cpp)
file(GLOB LUAMNGR_SRC ${FORGE_ROOT}Middleware_3/LUA/*.cpp ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/lua-5.3.5/src/*.c)
#file(GLOB_RECURSE OZZ_SRC ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/ozz-animation/src/*.cc ${FORGE_ROOT}Common_3/ThirdParty/OpenSource/ozz-animation/src/*.h)

add_library(luamngr_lib ${LUAMNGR_SRC})
#add_library(animation_lib ${ANIMATION_SRC} ${OZZ_SRC})
add_library(animation_lib ${ANIMATION_SRC})

add_library(renderer_lib STATIC ${RENDER_VULKAN_SRC}  ${RENDER_COMMON_SRC} ${OS_CORE_SRC} ${SPIRV_TOOLS_SRC} ${SPIRV_CROSS_SRC} ${OS_FS_SRC})
add_library(memtrack_lib STATIC ${OS_MEMTRACK_SRC})
add_library(eastl_lib STATIC ${EASTL_SRC} ${EASTDC_SRC})
add_library(log_lib STATIC ${OS_LOGGING_SRC})
add_library(zip_lib STATIC ${ZIP_SRC})
add_library(profiler_lib STATIC ${OS_PROFILER_SRC})
#add_library(os_lib STATIC ${OS_ANDROID_SRC} ${OS_CORE_SRC} ${OS_FS_SRC} ${RENDER_VULKAN_SRC} ${RENDER_COMMON_SRC})
add_library(os_lib STATIC ${OS_ANDROID_SRC} ${OS_FS_SRC})
add_library(input_lib STATIC ${OS_INPUT_SRC} ${GAINPUT_SRC} ${GAINPUT_KBD_SRC}
                             ${GAINPUT_PAD_SRC} ${GAINPUT_MOUSE_SRC} ${GAINPUT_TOUCH_SRC})
add_library(ui_lib STATIC ${MIDDLEWARE_UI_SRC} ${IMGUI_SRC} ${MIDDLEWARE_TEXT_SRC} ${MIDDLEWARE_PANINI_SRC}
                          ${OS_ANDROID_SRC}
                          ${BASISU_SRC})
add_library(lib_shaderc STATIC IMPORTED)
set_target_properties(lib_shaderc PROPERTIES IMPORTED_LOCATION
        ${ANDROID_NDK}/sources/third_party/shaderc/libs/c++_shared/arm64-v8a/libshaderc.a)


add_library(ozz_animation_lib STATIC IMPORTED)
set_target_properties(ozz_animation_lib PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/../../libs/libozz_animation.a)
add_library(ozz_base_lib STATIC IMPORTED)
set_target_properties(ozz_base_lib PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/../../libs/libozz_base.a)

include_directories(${ANDROID_NDK}/sources/android/native_app_glue)
include_directories(${ANDROID_NDK}/sources/third_party/shaderc/libshaderc/include)
include_directories(${FORGE_ROOT}Common_3/ThirdParty/OpenSource/gainput/lib/include)
add_library(theforgebase ${OS_CAMERA_SRC})
target_link_libraries(  theforgebase
                        os_lib
                        renderer_lib
                        memtrack_lib
                        #native_app_glue
                        log_lib
                        eastl_lib
                        zip_lib
                        profiler_lib
                        input_lib
                        ui_lib
                        lib_shaderc
                        ozz_animation_lib
                        ozz_base_lib
                        animation_lib
                        luamngr_lib)