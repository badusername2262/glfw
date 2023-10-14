cmake_minimum_required(VERSION 3.4...3.20 FATAL_ERROR)
project(GLFW VERSION 3.4.0 LANGUAGES C)

if (POLICY CMP0069)
    cmake_policy(SET CMP0069 NEW)
endif()

if (POLICY CMP0077)
    cmake_policy(SET CMP0077 NEW)
endif()

add_compile_options(-std=c11 -lgdi32)

set(files        include/GLFW/glfw3.h include/GLFW/glfw3native.h src/glfw_config.h src/context.c src/init.c src/input.c src/monitor.c src/vulkan.c src/window.c)
set(win32_files  src/win32_init.c src/win32_joystick.c src/win32_monitor.c src/win32_time.c src/win32_thread.c src/win32_window.c src/wgl_context.c src/egl_context.c src/osmesa_context.c)

add_library(GLFW STATIC ${files} ${win32_files})