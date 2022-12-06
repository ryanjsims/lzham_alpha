project(lzham)
cmake_minimum_required(VERSION 3.12)

if(MSVC)
    set(threading_src lzham_win32_threading.cpp)
else()
    set(threading_src lzham_pthreads_threading.cpp)
endif()

add_library(lzham STATIC 
    lzhamdecomp/lzham_assert.cpp
    lzhamdecomp/lzham_checksum.cpp
    lzhamdecomp/lzham_huffman_codes.cpp
    lzhamdecomp/lzham_lzdecompbase.cpp
    lzhamdecomp/lzham_lzdecomp.cpp
    lzhamdecomp/lzham_mem.cpp
    lzhamdecomp/lzham_platform.cpp
    lzhamdecomp/lzham_polar_codes.cpp
    lzhamdecomp/lzham_prefix_coding.cpp
    lzhamdecomp/lzham_symbol_codec.cpp
    lzhamdecomp/lzham_timer.cpp
    lzhamdecomp/lzham_vector.cpp
    lzhamcomp/lzham_lzbase.cpp
    lzhamcomp/lzham_lzcomp.cpp
    lzhamcomp/lzham_lzcomp_internal.cpp
    lzhamcomp/lzham_lzcomp_state.cpp
    lzhamcomp/lzham_match_accel.cpp
    lzhamcomp/lzham_lzcomp_internal.cpp
    lzhamcomp/${threading_src}
    lzhamlib/lzham_lib.cpp
)
target_include_directories(lzham 
    PUBLIC include lzhamdecomp lzhamcomp
)

if(NOT MSVC)
    target_compile_options(lzham PRIVATE "-Wno-unused-value")
endif()

