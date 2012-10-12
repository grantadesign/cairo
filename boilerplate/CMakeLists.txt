include(CMake.sources)
include(CMake.win32.features)

include_directories(../src)

set(cairo_boilerplate_constructors_src ${CMAKE_CURRENT_SOURCE_DIR}/cairo_boilerplate_constructors.c)
set_source_files_properties(${cairo_boilerplate_constructors_src} PROPERTIES GENERATED TRUE)

add_custom_command(COMMAND ${CYGWIN_INSTALL_PATH}/bin/sh ${CMAKE_CURRENT_SOURCE_DIR}/make-cairo-boilerplate-constructors.sh ${enabled_cairo_boilerplate_sources} > ${cairo_boilerplate_constructors_src}
                   OUTPUT ${cairo_boilerplate_constructors_src}
                   WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
                   
add_library(cairo_boilerplate STATIC ${enabled_cairo_boilerplate_sources} ${cairo_boilerplate_constructors_src})
SET_PROPERTY(TARGET cairo_boilerplate PROPERTY FOLDER "cairo/tests")