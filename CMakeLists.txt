cmake_minimum_required(VERSION 3.20)

# 工程名可自行修改；正式项目建议改成有意义的英文名
project(cpp_practice LANGUAGES CXX)

# ---- C++ 标准 ----
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)   # 用 -std=c++17 而非 -std=gnu++17，保证可移植

# ---- 输出目录：可执行文件统一放到 build/bin ----
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# ---- 默认开启常用警告 ----
if(NOT MSVC)
    add_compile_options(-Wall -Wextra)
endif()

# ---- 可执行目标 ----
# 新增源文件时，直接追加到 add_executable 里即可
add_executable(hello
    abs.cpp
)

# ---- MinGW 下静态链接运行库，让 exe 不依赖 DLL、可直接分发 ----
if(MINGW)
    target_link_options(hello PRIVATE -static -static-libgcc -static-libstdc++)
endif()

# 需要链接的库写在这里，例如：
# target_link_libraries(hello PRIVATE somelib)
