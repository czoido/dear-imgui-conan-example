cmake_minimum_required(VERSION 3.0)
project(dear-imgui-conan CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable( dear-imgui-conan 
                main.cpp 
                
				bindings/imgui_impl_glfw.cpp
				bindings/imgui_impl_opengl3.cpp
				opengl_shader.cpp
				file_manager.cpp
						
				bindings/imgui_impl_glfw.h
				bindings/imgui_impl_opengl3.h 
				bindings/imgui_impl_opengl3_loader.h
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
