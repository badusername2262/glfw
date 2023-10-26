cmake_minimum_required(VERSION 3.4...3.20 FATAL_ERROR)
project(GLFW VERSION 3.4.0 LANGUAGES C)

set(LIBRARY_OUTPUT_PATH ../../../bin/x86_64/lib)

if (POLICY CMP0069)
    cmake_policy(SET CMP0069 NEW)
endif()

if (POLICY CMP0077)
    cmake_policy(SET CMP0077 NEW)
endif()

add_compile_options(-std=c17 -lgdi32)
add_compile_definitions(_GLFW_WIN32 _CRT_SECURE_NO_WARNINGS)

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

add_library(GLFW STATIC ${files} ${win32_files})