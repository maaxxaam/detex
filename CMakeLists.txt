cmake_minimum_required(VERSION 3.20)
project(detex)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(detex_src
    bits.c
    clamp.c
    dds.c
    decompress-bptc.c
    decompress-eac.c
    decompress-rgtc.c
    file-info.c
    hdr.c
    misc.c
    raw.c
    bptc-tables.c
    convert.c
    decompress-bc.c
    decompress-bptc-float.c
    decompress-etc.c
    division-tables.c
    half-float.c
    ktx.c
    texture.c
)
add_library(detex STATIC ${detex_src})

if (NOT MSVC)
    add_executable(detex-validate validate.c)
    target_link_libraries(detex-validate PRIVATE detex)

    add_executable(detex-view detex-view.c)
    target_link_libraries(detex-view PRIVATE detex)

    find_package(PNG)
    if (PNG_FOUND)
        add_executable(detex-convert detex-convert.c png.c)
        target_link_libraries(detex-convert PRIVATE detex PNG::PNG)
    endif()
endif()
