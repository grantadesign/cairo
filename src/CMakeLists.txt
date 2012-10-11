include(CMake.sources)
include(CMake.win32.features)

add_definitions(
	-D_CRT_SECURE_NO_DEPRECATE
	-D_CRT_NONSTDC_NO_DEPRECATE
)

#for pnglibconf.h, which is generated during libpng build, and not available in the source tree.
include_directories("${GATEWAYDEPS_BINARY_DIR}/libpng"
                    .)
                    
add_library(cairo SHARED ${enabled_cairo_sources})

target_link_libraries(cairo zlib png15 pixman gdi32 msimg32 pthreadsVC2) #pthreads needed due to pixman

SET_PROPERTY(TARGET cairo PROPERTY FOLDER "cairo")

add_dependencies(cairo UPDATE_CAIRO_FEATURES_H)
