cmake_minimum_required(VERSION 3.31)
set(CMAKE_PROJECT_TOP_LEVEL_INCLUDES .devcontainer/cmake/xproinc.cmake)
project(libexpat)
string(JOIN "\n" ALIASES
  "if(NOT TARGET EXPAT::EXPAT)"
  "  add_library(EXPAT::EXPAT ALIAS ${XP_NAMESPACE}::expat)"
  "endif()"
  ""
  )
set(targetsFile ${PROJECT_NAME}-targets)
xpExternPackage(NAMESPACE ${XP_NAMESPACE}
  TARGETS_FILE ${targetsFile} LIBRARIES expat
  BASE R_2_2_5 XPDIFF "patch"
  WEB "https://libexpat.github.io" UPSTREAM "github.com/libexpat/libexpat"
  DESC "a stream-oriented XML parser library written in C"
  LICENSE "[MIT](https://github.com/libexpat/libexpat/blob/R_2_2_5/expat/COPYING 'MIT License')"
  )
add_subdirectory(expat)
