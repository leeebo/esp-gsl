idf_component_register(INCLUDE_DIRS ${COMPONENT_DIR}/include)
add_dependencies(${COMPONENT_LIB} gslcblas gsl)
target_link_libraries( ${COMPONENT_LIB} INTERFACE ${COMPONENT_DIR}/lib/libgsl.a ${COMPONENT_DIR}/lib/libgslcblas.a)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fpic")

externalproject_add(gsl_build
    PREFIX ${COMPONENT_DIR}
    TMP_DIR ${COMPONENT_DIR}/build/tmp
    STAMP_DIR ${COMPONENT_DIR}/build/stamp
    SOURCE_DIR "${COMPONENT_DIR}/gsl-2.7.1"
    CONFIGURE_COMMAND "${COMPONENT_DIR}/gsl-2.7.1/configure" "--host=xtensa" "--disable-doc" "--prefix=${COMPONENT_DIR}"
    BUILD_ALWAYS 1
    BUILD_COMMAND make CC=${CMAKE_C_COMPILER} CFLAGS=${CMAKE_C_FLAGS}
    BUILD_BYPRODUCTS ${COMPONENT_DIR}/lib ${COMPONENT_DIR}/include
    INSTALL_COMMAND make CC=${CMAKE_C_COMPILER} CFLAGS=${CMAKE_C_FLAGS} install libdir=${COMPONENT_DIR}/lib includedir=${COMPONENT_DIR}/include
)

# Add libgsl.a to the build process
add_library(gsl STATIC IMPORTED GLOBAL)
add_dependencies(gsl gsl_build)
add_library(gslcblas STATIC IMPORTED GLOBAL)
add_dependencies(gslcblas gsl_build)

set_target_properties(gsl PROPERTIES IMPORTED_LOCATION
    ${COMPONENT_DIR}/lib/libgsl.a)
set_target_properties(gslcblas PROPERTIES IMPORTED_LOCATION
    ${COMPONENT_DIR}/lib/libgslcblas.a)
set_target_properties(gsl PROPERTIES INTERFACE_INCLUDE_DIRECTORIES
    ${COMPONENT_DIR}/include)
set_target_properties(gslcblas PROPERTIES INTERFACE_INCLUDE_DIRECTORIES
    ${COMPONENT_DIR}/include)
set_property(DIRECTORY PROPERTY ADDITIONAL_MAKE_CLEAN_FILES
    ${COMPONENT_DIR}/lib/libgsl.a ${COMPONENT_DIR}/lib/libgslcblas.a ${COMPONENT_DIR}/gsl-2.7.1/libgsl.a ${COMPONENT_DIR}/gsl-2.7.1/libgslcblas.a)