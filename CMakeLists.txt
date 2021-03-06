cmake_minimum_required(VERSION 2.8.12)
project(dear-imgui-conan)

include(${CMAKE_BINARY_DIR}/conanbuildinfo_multi.cmake)
conan_basic_setup()

add_executable( dear-imgui-conan 
                main.cpp 
                bindings/imgui_impl_glfw.cpp
                bindings/imgui_impl_opengl3.cpp
                opengl_shader.cpp
				file_manager.cpp
                bindings/imgui_impl_glfw.h
                bindings/imgui_impl_opengl3.h 
                opengl_shader.h 
				file_manager.h 
				assets/simple-shader.vs
				assets/simple-shader.fs )

add_custom_command(TARGET dear-imgui-conan
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_SOURCE_DIR}/assets/simple-shader.vs ${PROJECT_BINARY_DIR}
    COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_SOURCE_DIR}/assets/simple-shader.fs ${PROJECT_BINARY_DIR}
)

target_compile_definitions(dear-imgui-conan PUBLIC IMGUI_IMPL_OPENGL_LOADER_GLEW)

conan_target_link_libraries(dear-imgui-conan)
