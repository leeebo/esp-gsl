# The following lines of boilerplate have to be in your project's
# CMakeLists in this exact order for cmake to work correctly
cmake_minimum_required(VERSION 3.5)
project(buil_esp_gsl_lib)
include(ExternalProject)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fpic")
externalproject_add(gsl_build
    PREFIX ${LIB_IST_PATH}/gsl_build/${IDF_TARGET}
    TMP_DIR ${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/tmp
    STAMP_DIR ${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/stamp
    SOURCE_DIR "${CMAKE_CURRENT_LIST_DIR}/../gsl-2.7.1"
    CONFIGURE_COMMAND "${CMAKE_CURRENT_LIST_DIR}/../gsl-2.7.1/configure" "--host=xtensa" "--prefix=${LIB_IST_PATH}/gsl_build/${IDF_TARGET}"
    BUILD_ALWAYS 1
    BUILD_BYPRODUCTS ${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/lib ${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/include
    BUILD_COMMAND make CC=${CMAKE_C_COMPILER} CFLAGS=${CMAKE_C_FLAGS}
    INSTALL_COMMAND make CC=${CMAKE_C_COMPILER} CFLAGS=${CMAKE_C_FLAGS} install libdir=${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/lib includedir=${LIB_IST_PATH}/gsl_build/${IDF_TARGET}/include
)
