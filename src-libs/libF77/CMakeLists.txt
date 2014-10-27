# Copyright (c) 2014 by AppSmiths Ventures LLP.  All Rights Reserved.
#
# All material is proprietary to AppSmiths Ventures LLP and may be used only
# pursuant to license rights granted by AppSmiths Ventures LLP  Other
# reproduction, distribution, or use is strictly prohibited.
#
cmake_minimum_required(VERSION 3.30)
project(libF77 C)

set(libname "F77")

if (BUILD_SHARED_LIB)
    add_library(${libname} SHARED)
    target_link_libraries(${libname} PRIVATE I77)
    set_target_properties(${libname} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
    if (MSVC)
        target_compile_definitions(${libname} PRIVATE _CRT_SECURE_NO_WARNINGS)
    endif (MSVC)
    if (UNIX)
        # force linker to resolve all deps
        #        set_target_properties(${libname} PROPERTIES LINK_FLAGS "-Wl,--no-undefined")
    endif (UNIX)
else (BUILD_SHARED_LIB)
    add_library(${libname})
endif (BUILD_SHARED_LIB)

if (WIN32)
    target_compile_definitions(${libname} PRIVATE MSDOS)
    if (MSVC)
        install(FILES $<TARGET_PDB_FILE:${libname}> DESTINATION bin OPTIONAL)
    endif (MSVC)
endif (WIN32)
target_compile_definitions(${libname} PUBLIC INTEGER_STAR_8)
#DNO_LONG_LONG
target_include_directories(${libname} PRIVATE ../..)
target_sources(${libname} PRIVATE
    abort_.c
    c_abs.c
    c_cos.c
    c_div.c
    c_exp.c
    c_log.c
    c_sin.c
    c_sqrt.c
    cabs.c
    d_abs.c
    d_acos.c
    d_asin.c
    d_atan.c
    d_atn2.c
    d_cnjg.c
    d_cos.c
    d_cosh.c
    d_dim.c
    d_exp.c
    d_imag.c
    d_int.c
    d_lg10.c
    d_log.c
    d_mod.c
    d_nint.c
    d_prod.c
    d_sign.c
    d_sin.c
    d_sinh.c
    d_sqrt.c
    d_tan.c
    d_tanh.c
    derf_.c
    derfc_.c
    dtime_.c
    ef1asc_.c
    ef1cmc_.c
    erf_.c
    erfc_.c
    etime_.c
    exit_.c
    F77_aloc.c
    f77vers.c
    getenv_.c
    h_abs.c
    h_dim.c
    h_dnnt.c
    h_indx.c
    h_len.c
    h_mod.c
    h_nint.c
    h_sign.c
    hl_ge.c
    hl_gt.c
    hl_le.c
    hl_lt.c
    i_abs.c
    i_dim.c
    i_dnnt.c
    i_indx.c
    i_len.c
    i_mod.c
    i_nint.c
    i_sign.c
    l_ge.c
    l_gt.c
    l_le.c
    l_lt.c
    lbitbits.c
    lbitshft.c
    pow_ci.c
    pow_dd.c
    pow_di.c
    pow_hh.c
    pow_ii.c
    pow_qq.c
    pow_ri.c
    pow_zi.c
    pow_zz.c
    qbitbits.c
    qbitshft.c
    r_abs.c
    r_acos.c
    r_asin.c
    r_atan.c
    r_atn2.c
    r_cnjg.c
    r_cos.c
    r_cosh.c
    r_dim.c
    r_exp.c
    r_imag.c
    r_int.c
    r_lg10.c
    r_log.c
    r_mod.c
    r_nint.c
    r_sign.c
    r_sin.c
    r_sinh.c
    r_sqrt.c
    r_tan.c
    r_tanh.c
    s_cat.c
    s_cmp.c
    s_copy.c
    s_paus.c
    s_rnge.c
    s_stop.c
    signal_.c
    system_.c
    uninit.c
    z_abs.c
    z_cos.c
    z_div.c
    z_exp.c
    z_log.c
    z_sin.c
    z_sqrt.c
)

install(TARGETS ${libname}
	ARCHIVE DESTINATION lib
       	LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin
	)
