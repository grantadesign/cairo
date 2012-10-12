include(CMake.sources)

include_directories(.
                    ../src
                    ../boilerplate
                    ../util
                    ../util/cairo-script
                    pdiff)

set(pdiff_srcs pdiff/lpyramid.c pdiff/pdiff.c)

set(cairo_test_constructors_src ${CMAKE_CURRENT_SOURCE_DIR}/cairo_test_constructors.c)
set_source_files_properties(${cairo_test_constructors_src} PROPERTIES GENERATED TRUE)

add_custom_command(COMMAND ${CYGWIN_INSTALL_PATH}/bin/sh ${CMAKE_CURRENT_SOURCE_DIR}/make-cairo-test-constructors.sh ${test_sources} > ${cairo_test_constructors_src}
                   OUTPUT ${cairo_test_constructors_src}
                   WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})

add_executable(cairo_testsuite ${test_sources} ${cairo_test_suite_sources} ${pdiff_srcs} ${cairo_test_constructors_src})
target_link_libraries(cairo_testsuite cairo cairo_boilerplate)
add_test(cairo_testsuite ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/cairo_testsuite)
SET_PROPERTY(TARGET cairo_testsuite PROPERTY FOLDER "cairo/tests")

add_definitions(-DCAIRO_WIN32_STATIC_BUILD)
add_executable(any2ppm any2ppm.c)
target_link_libraries(any2ppm cairo cairo_boilerplate cairo_script)

SET_PROPERTY(TARGET any2ppm PROPERTY FOLDER "cairo/tests")

