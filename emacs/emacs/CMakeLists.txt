include(ExternalProject)

ExternalProject_Add (
  emacs

  PREFIX              emacs
  URL                 http://ftp.gnu.org/gnu/emacs/emacs-26.3.tar.gz
  
  BUILD_ALWAYS        OFF
  INSTALL_DIR         ${PROJECT_BINARY_DIR}/external_staging
  CONFIGURE_COMMAND   ${CMAKE_CURRENT_BINARY_DIR}/emacs/src/emacs/configure --prefix=<INSTALL_DIR> --with-gnutls=no
  BUILD_COMMAND       make -j10
  BUILD_IN_SOURCE     1
)

# We have to use relative paths for the DESTINATION (which are
# interpreted as being relative to ${CMAKE_INSTALL_PREFIX}), so that
# CPack will work
install(DIRECTORY ${PROJECT_BINARY_DIR}/external_staging/lib
       DESTINATION ${flavorqual_dir}
       USE_SOURCE_PERMISSIONS)
install(DIRECTORY ${PROJECT_BINARY_DIR}/external_staging/include
       DESTINATION ${flavorqual_dir}
       USE_SOURCE_PERMISSIONS)
install(DIRECTORY ${PROJECT_BINARY_DIR}/external_staging/bin
       DESTINATION ${flavorqual_dir}
       USE_SOURCE_PERMISSIONS)
install(DIRECTORY ${PROJECT_BINARY_DIR}/external_staging/share
       DESTINATION ${flavorqual_dir}
       USE_SOURCE_PERMISSIONS)
