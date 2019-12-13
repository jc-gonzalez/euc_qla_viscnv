#======================================================================
# CMakeLists.txt
# QPF - Prototype of QLA Processing Framework
# General Project File
#======================================================================
# Author: J C Gonzalez - 2015-2018
# Copyright (C) 2015-2018 Euclid SOC Team at ESAC
#======================================================================

project (viscnv)

#-----------------------------------------------------------------
cmake_minimum_required(VERSION 2.8.2)
cmake_policy (SET CMP0015 NEW)

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set (PWD ${viscnv_SOURCE_DIR})

set (HTOOLS_ROOT_DIR  ${PWD}/../htools)
set (LOG_ROOT_DIR     ${PWD}/../log)
set (Q_ROOT_DIR       ${PWD}/../q)

INCLUDE_DIRECTORIES (. /usr/include $ENV{HOME}/opt/include)
LINK_DIRECTORIES (/usr/lib64 /usr/lib $ENV{HOME}/opt/lib)
#-----------------------------------------------------------------

set (viscnv_hdr
ccd_id.h
compr_info.h
config_tables.h
expo_duration.h
le1_vis_ccd.h
raw_vis_hdr.h
raw_vis_scipckt.h
tcparams.h
types.h
ver_seqconf.h
vis_base.h
vis_converter.h
)

set (viscnv_src
main.cpp
ccd_id.cpp
compr_info.cpp
config_tables.cpp
expo_duration.cpp
le1_vis_ccd.cpp
raw_vis_hdr.cpp
raw_vis_scipckt.cpp
tcparams.cpp
types.cpp
ver_seqconf.cpp
vis_base.cpp
vis_converter.cpp
)

set (SZIP_DIR /home/eucops/opt)
set (SZIP_INC_DIR ${SZIP_DIR}/include)
set (SZIP_LIB_DIR ${SZIP_DIR}/lib)

set (CFITSIO_DIR /usr)
set (CFITSIO_INC_DIR ${CFITSIO_DIR}/include/cfitsio)
set (CFITSIO_LIB_DIR ${CFITSIO_DIR}/lib64)

add_executable(viscnv ${viscnv_src})
target_include_directories (viscnv PUBLIC . ..
  ${Q_ROOT_DIR}
  ${LOG_ROOT_DIR}
  ${HTOOLS_ROOT_DIR}
  ${SZIP_INC_DIR}
  ${CFITSIO_INC_DIR}
)
target_link_libraries (viscnv
  q log
  sz curl cfitsio m)

set_target_properties (viscnv PROPERTIES LINKER_LANGUAGE CXX)
install (TARGETS viscnv
         RUNTIME DESTINATION bin
         ARCHIVE DESTINATION lib
         LIBRARY DESTINATION lib)
