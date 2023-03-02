# External build process for quirc, runs in source dir and
# produces libquirc.a
idf_component_register(INCLUDE_DIRS  ${COMPONENT_DIR}/include)
externalproject_add(gsl_build
    PREFIX ${COMPONENT_DIR}
    TMP_DIR ${COMPONENT_DIR}/build/tmp
    STAMP_DIR ${COMPONENT_DIR}/build/stamp
    SOURCE_DIR "${COMPONENT_DIR}/gsl_2_7"
    CONFIGURE_COMMAND "${COMPONENT_DIR}/gsl_2_7/configure" "--host=xtensa" 
    BUILD_IN_SOURCE 1
    BUILD_ALWAYS 1
    BUILD_COMMAND make CC=${CMAKE_C_COMPILER} CXX=${CMAKE_CXX_COMPILER} {CFLAGS=${CMAKE_C_FLAGS}}   CXXLAGS=${CMAKE_CXX_FLAGS}  AR=${CMAKE_AR} 
    INSTALL_COMMAND make CC=${CMAKE_C_COMPILER} CFLAGS=${CMAKE_C_FLAGS} AR=${CMAKE_AR} install libdir=${COMPONENT_DIR}/lib includedir=${COMPONENT_DIR}/include
    )

# Add libgsl.a to the build process
add_library(gsl STATIC IMPORTED GLOBAL)
add_dependencies(gsl gsl_build)

set_target_properties(gsl PROPERTIES IMPORTED_LOCATION
    ${COMPONENT_DIR}/lib/libgsl.a  )
set_target_properties(gsl PROPERTIES IMPORTED_LOCATION
    ${COMPONENT_DIR}/lib/libgslcblas.a  )
set_target_properties(gsl PROPERTIES INTERFACE_INCLUDE_DIRECTORIES
    ${COMPONENT_DIR}/include)

 target_link_libraries( ${COMPONENT_LIB} INTERFACE ${COMPONENT_DIR}/lib/libgsl.a ${COMPONENT_DIR}/lib/libgslcblas.a)

# set_directory_properties( PROPERTIES ADDITIONAL_MAKE_CLEAN_FILES
#     "${COMPONENT_DIR}/gsl_2_7/libgsl.a")
    