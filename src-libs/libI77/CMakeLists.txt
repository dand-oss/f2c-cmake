# Copyright (c) 2014 by AppSmiths Ventures LLP.  All Rights Reserved.
#
# All material is proprietary to AppSmiths Ventures LLP and may be used only
# pursuant to license rights granted by AppSmiths Ventures LLP  Other
# reproduction, distribution, or use is strictly prohibited.
#
cmake_minimum_required(VERSION 3.1)
project(libI77 C)

set(libname "I77")

if (BUILD_SHARED_LIB)
    add_library(${libname} SHARED)
    set_target_properties(${libname} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
    if (MSVC)
        target_compile_definitions(${libname} PRIVATE _CRT_SECURE_NO_WARNINGS)
    endif (MSVC)
    if (UNIX)
        # force linker to resolve all deps
        set_target_properties(${libname} PROPERTIES LINK_FLAGS "-Wl,--no-undefined")
    endif (UNIX)
else (BUILD_SHARED_LIB)
    add_library(${libname})
endif (BUILD_SHARED_LIB)

if (WIN32)
    target_compile_definitions(${libname} PRIVATE MSDOS)
    target_compile_definitions(${libname} PRIVATE SYSDEP_H_INCLUDED)
    if (MSVC)
        install(FILES $<TARGET_PDB_FILE:${libname}> DESTINATION bin OPTIONAL)
    endif (MSVC)
endif (WIN32)
target_compile_definitions(${libname} PUBLIC INTEGER_STAR_8)
#DNO_LONG_LONG
target_include_directories(${libname} PRIVATE ../..)
target_sources(${libname} PRIVATE
    backspace.c
    close.c
    dfe.c
    dolio.c
    due.c
    endfile.c
    err.c
    fmt.c
    fmtlib.c
    ftell_.c
    ftell64_.c
    i77vers.c
    iio.c
    ilnw.c
    inquire.c
    lread.c
    lwrite.c
    open.c
    rdfmt.c
    rewind.c
    rsfe.c
    rsli.c
    rsne.c
    sfe.c
    signbit.c
    sue.c
    typesize.c
    uio.c
    util.c
    wref.c
    wrtfmt.c
    wsfe.c
    wsle.c
    wsne.c
    xwsne.c
    sig_die.c
    )

install(TARGETS ${libname}
	ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
	RUNTIME DESTINATION bin
	)
