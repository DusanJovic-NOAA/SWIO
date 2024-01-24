
###############################################################################
### COMIO
###############################################################################

add_subdirectory(COMIO)

###############################################################################
### UFSIO
###############################################################################

add_library(ufsio
  src/swio.F90
  src/swio_calculator.F90
  src/swio_data.F90
  src/swio_methods.F90
)

add_dependencies(ufsio comio)

target_link_libraries(ufsio PUBLIC comio)

set_target_properties(ufsio PROPERTIES Fortran_MODULE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/mod)
target_include_directories(ufsio INTERFACE $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/mod>
                                           $<INSTALL_INTERFACE:mod>)


###############################################################################
### Install
###############################################################################
install(
  TARGETS ufsio
  EXPORT ufsio-config
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)

install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/mod DESTINATION ${CMAKE_INSTALL_PREFIX})

install(EXPORT ufsio-config
  DESTINATION lib/cmake)
