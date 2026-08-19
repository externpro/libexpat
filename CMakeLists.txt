cmake_minimum_required(VERSION 4.3)
project(libexpat)
string(JOIN "\n" ALIASES
  "if(NOT TARGET EXPAT::EXPAT)"
  "  add_library(EXPAT::EXPAT ALIAS ${CMAKE_PROJECT_NAME}::expat)"
  "endif()"
  ""
  )
set(targetsFile ${PROJECT_NAME}-targets)
add_subdirectory(expat)
if(COMMAND xpExternPackage)
  xpExternPackage(TARGETS_FILE ${targetsFile}
    LIBRARIES expat DEFAULT_TARGETS expat
    BASE R_2_2_5 XPDIFF "patch"
    WEB "https://libexpat.github.io" UPSTREAM "github.com/libexpat/libexpat"
    DESC "a stream-oriented XML parser library written in C"
    LICENSE "[MIT](https://github.com/libexpat/libexpat/blob/R_2_2_5/expat/COPYING 'MIT License')"
    )
  expat_install(EXPORT ${targetsFile} DESTINATION ${CMAKE_INSTALL_CMAKEDIR} NAMESPACE ${CMAKE_PROJECT_NAME}::)
endif()
