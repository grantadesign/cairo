include(CMake.sources)

include_directories(../../src)
                    
add_definitions(-DCAIRO_WIN32_STATIC_BUILD)
                    
add_library(cairo_script STATIC ${libcairo_script_interpreter_sources} ${libcairo_script_interpreter_headers})
SET_PROPERTY(TARGET cairo_script PROPERTY FOLDER "cairo/tests")