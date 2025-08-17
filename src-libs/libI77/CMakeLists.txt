cmake_minimum_required(VERSION 3.30)

project(libI77
    VERSION 1.1.0
    LANGUAGES C
)

set(libname "I77")

if (BUILD_SHARED_LIB)
    add_library(${libname} SHARED)
    set_target_properties(${libname}
        PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON
    )
    if (MSVC)
        target_compile_definitions(${libname}
            PRIVATE _CRT_SECURE_NO_WARNINGS
        )
    endif()
    if (UNIX)
        set_target_properties(${libname}
            PROPERTIES LINK_FLAGS "-Wl,--no-undefined"
        )
    endif()
else()
    add_library(${libname} STATIC)
endif()

if (WIN32)
    target_compile_definitions(${libname}
        PRIVATE MSDOS SYSDEP_H_INCLUDED
    )
    if (MSVC)
        install(FILES $<TARGET_PDB_FILE:${libname}>
            DESTINATION ${CMAKE_INSTALL_BINDIR}
            OPTIONAL
        )
    endif()
endif()

target_compile_definitions(${libname}
    PUBLIC INTEGER_STAR_8
)

target_include_directories(${libname}
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/libI77>
)

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

# Install library and register in f2cTargets
install(TARGETS ${libname}
    EXPORT f2cTargets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# Install public headers for libI77
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/libI77
    FILES_MATCHING PATTERN "*.h"
)
