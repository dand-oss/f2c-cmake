# Copyright (c) 2014 by AppSmiths Ventures LLP.  All Rights Reserved.
#
# All material is proprietary to AppSmiths Ventures LLP and may be used only
# pursuant to license rights granted by AppSmiths Ventures LLP  Other
# reproduction, distribution, or use is strictly prohibited.
#
cmake_minimum_required(VERSION 3.30)
project(f2c-exe VERSION 1.0.0 LANGUAGES C)

set(exename "f2c")

#DNO_LONG_LONG

add_executable(${exename})

if (MSVC)
    target_compile_definitions(${exename} PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()

if (WIN32)
    target_compile_definitions(${exename} PRIVATE MSDOS)
endif()

target_include_directories(${exename} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/..>
)

target_sources(${exename} PRIVATE
    cds.c
    data.c
    equiv.c
    error.c
    exec.c
    expr.c
    format.c
    formatdata.c
    gram.c
    init.c
    intr.c
    io.c
    lex.c
    main.c
    mem.c
    misc.c
    names.c
    niceprintf.c
    output.c
    p1output.c
    parse_args.c
    pread.c
    proc.c
    put.c
    putpcc.c
    sysdep.c
    vax.c
    version.c
)

# Install executable and register in f2cTargets
install(TARGETS ${exename}
    EXPORT f2cTargets
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)