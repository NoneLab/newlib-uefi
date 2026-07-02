cmake_minimum_required(VERSION 3.20)

project(libc_uefi LANGUAGES C CXX)

add_library(c_uefi STATIC)

target_sources(c_uefi PRIVATE
    newlib/libc/string/memchr.c
    newlib/libc/string/memcmp.c
    newlib/libc/string/memcpy.c
    newlib/libc/string/memmove.c
    newlib/libc/string/memset.c
    newlib/libc/string/strcat.c
    newlib/libc/string/strchr.c
    newlib/libc/string/strcmp.c
    newlib/libc/string/strcoll.c
    newlib/libc/string/strcpy.c
    newlib/libc/string/strcspn.c
    newlib/libc/string/strerror.c
    newlib/libc/string/strlen.c
    newlib/libc/string/strncat.c
    newlib/libc/string/strncmp.c
    newlib/libc/string/strncpy.c
    newlib/libc/string/strpbrk.c
    newlib/libc/string/strrchr.c
    newlib/libc/string/strspn.c
    newlib/libc/string/strstr.c
    newlib/libc/string/strtok.c
    newlib/libc/string/strxfrm.c
    newlib/libc/string/strcoll_l.c
    newlib/libc/string/strxfrm_l.c
    newlib/libc/string/strtok_r.c
    newlib/libc/string/timingsafe_bcmp.c
    newlib/libc/string/timingsafe_memcmp.c
    newlib/libc/string/memccpy.c
    newlib/libc/string/memmem.c
    newlib/libc/string/stpcpy.c
    newlib/libc/string/stpncpy.c
    newlib/libc/string/strdup.c
    newlib/libc/string/strdup_r.c
    newlib/libc/string/strndup.c
    newlib/libc/string/strndup_r.c
    newlib/libc/string/strerror_r.c
    newlib/libc/string/strlcat.c
    newlib/libc/string/strlcpy.c
    newlib/libc/string/strnlen.c
    newlib/libc/string/strsep.c
    newlib/libc/string/strnstr.c
    newlib/libc/string/strlwr.c
    newlib/libc/string/strupr.c
    newlib/libc/string/strsignal.c

)

target_compile_features(c_uefi PRIVATE cxx_std_26)

target_compile_options(c_uefi PRIVATE
    -ffreestanding
    -fno-stack-protector
    -fno-builtin
    -mno-red-zone
    -Wall
    -Wextra
)

target_include_directories(c_uefi PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/newlib/libc/include
)

target_compile_options(c_uefi PRIVATE
    $<$<COMPILE_LANGUAGE:CXX>:-fno-exceptions>
    $<$<COMPILE_LANGUAGE:CXX>:-fno-rtti>
    $<$<COMPILE_LANGUAGE:CXX>:-fno-threadsafe-statics>
)

target_compile_definitions(c_uefi PRIVATE
    NEWLIB_UEFI_CLANG
)

target_link_options(c_uefi PRIVATE
    -nostdlib
    -fuse-ld=lld
)

# add_custom_command(TARGET simplefi POST_BUILD
#     COMMAND llvm-readobj --file-headers $<TARGET_FILE:simplefi>
#     COMMENT "Inspecting generated UEFI PE/COFF image"
# )
