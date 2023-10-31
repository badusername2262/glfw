cmake_minimum_required(VERSION 3.4...3.20 FATAL_ERROR)
project(GLFW VERSION 3.4.0 LANGUAGES C)

set(LIBRARY_OUTPUT_PATH ../../../bin)

if (POLICY CMP0069)
    cmake_policy(SET CMP0069 NEW)
endif()

if (POLICY CMP0077)
    cmake_policy(SET CMP0077 NEW)
endif()

if(CMAKE_GENERATOR MATCHES "Visual Studio 17 2022")
else()
    add_compile_options(-std=c11 -lgdi32)
endif()

if(GLFW_BUILD_WIN32)
    add_compile_definitions(_GLFW_WIN32 _CRT_SECURE_NO_WARNINGS)
endif()
if(GLFW_BUILD_X11)
    add_compile_definitions(_GLFW_X11)
endif()

set(files
        include/GLFW/glfw3.h
        include/GLFW/glfw3native.h
        src/context.c
        src/init.c
        src/input.c
        src/monitor.c

        src/null_init.c
        src/null_joystick.c
        src/null_monitor.c
        src/null_window.c

        src/platform.c
        src/vulkan.c
        src/window.c)

set(win32_files
        src/win32_init.c
        src/win32_joystick.c
        src/win32_module.c
        src/win32_monitor.c
        src/win32_time.c
        src/win32_thread.c
        src/win32_window.c
        src/wgl_context.c
        src/egl_context.c
        src/osmesa_context.c)

set(x11_files
        src/x11_platform.h
        src/xkb_unicode.h
        src/x11_init.c
        src/x11_monitor.c
        src/x11_window.c
        src/xkb_unicode.c
        src/posix_time.h
        src/posix_poll.c
        src/posix_time.c
        src/posix_thread.c
        src/posix_module.c
        src/glx_context.c
        src/egl_context.c
        src/osmesa_context.c
        src/linux_joystick.c)

if(GLFW_BUILD_WIN32)
    message(STATUS "Building for Windows")
    add_library(GLFW STATIC ${files} ${win32_files})
endif()
if(GLFW_BUILD_X11)
    message(STATUS "Building for Linux")
    add_library(GLFW STATIC ${files} ${x11_files})
endif()