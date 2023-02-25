# External build process for quirc, runs in source dir and
# produces libquirc.a
idf_component_register()
externalproject_add(gsl_build
    PREFIX ${COMPONENT_DIR}
    TMP_DIR ${COMPONENT_DIR}/build/tmp
    STAMP_DIR ${COMPONENT_DIR}/build/stamp
    SOURCE_DIR "${COMPONENT_DIR}/gsl-2.7.1"
    CONFIGURE_COMMAND "${COMPONENT_DIR}/gsl-2.7.1/configure"
    BUILD_IN_SOURCE 1
    BUILD_ALWAYS 1
    BUILD_COMMAND make CC=${CMAKE_C_COMPILER}
    INSTALL_COMMAND ""
    )

# Add libgsl.a to the build process
add_library(gsl STATIC IMPORTED GLOBAL)
add_dependencies(gsl gsl_build)

set_target_properties(gsl PROPERTIES IMPORTED_LOCATION
    ${COMPONENT_DIR}/gsl-2.7.1/libgsl.a)
set_target_properties(gsl PROPERTIES INTERFACE_INCLUDE_DIRECTORIES
    ${COMPONENT_DIR}/gsl-2.7.1/lib)

set_directory_properties( PROPERTIES ADDITIONAL_MAKE_CLEAN_FILES
    "${COMPONENT_DIR}/gsl-2.7.1/libgsl.a")