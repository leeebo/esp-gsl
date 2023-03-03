idf_component_register()
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR} ${CMAKE_MODULE_PATH} PARENT_SCOPE)
# Configure external project
execute_process(
    COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_BINARY_DIR}/gsl_build
)

execute_process(
    COMMAND ${CMAKE_COMMAND} -DLIB_IST_PATH=${CMAKE_BINARY_DIR} -DIDF_TARGET=${IDF_TARGET} ${CMAKE_CURRENT_LIST_DIR}/build_lib
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/gsl_build
)
# Build external project
execute_process(
    COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR}/gsl_build
)
