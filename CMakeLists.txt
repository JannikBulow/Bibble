cmake_minimum_required(VERSION 3.26)
project(Bibble VERSION 0.1.0)

set(CPACK_PACKAGE_NAME "bibble")
set(CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Bibble SDK")
set(CPACK_PACKAGE_CONTACT "jannikbulow0@gmail.com")
set(CPACK_GENERATOR "DEB")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Jannik Bülow")
set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)
set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)

include(CMakePackageConfigHelpers)
include(CPack)
include (FetchContent)

FetchContent_Declare(BibbleBytecode
    GIT_REPOSITORY https://github.com/JannikBulow/BibbleBytecode.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_Declare(BibbleOpcodes
    GIT_REPOSITORY https://github.com/JannikBulow/BibbleOpcodes.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_Declare(BibbleVM
    GIT_REPOSITORY https://github.com/JannikBulow/BibbleVM.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_Declare(BibbleASM
    GIT_REPOSITORY https://github.com/JannikBulow/BibbleASM.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_Declare(BibblIR
    GIT_REPOSITORY https://github.com/JannikBulow/BibblIR.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_Declare(BibbleC
    GIT_REPOSITORY https://github.com/JannikBulow/BibbleC.git
    GIT_TAG        master
    GIT_SHALLOW    TRUE
)

FetchContent_MakeAvailable(BibbleBytecode BibbleOpcodes BibbleVM BibbleASM BibblIR BibbleC)

configure_package_config_file(
    cmake/BibbleConfig.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/BibbleConfig.cmake"
    INSTALL_DESTINATION lib/cmake/Bibble
)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/BibbleConfigVersion.cmake"
    VERSION "${PROJECT_VERSION}"
    COMPATIBILITY SameMajorVersion
)

install(
    FILES
    "${CMAKE_CURRENT_BINARY_DIR}/BibbleConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/BibbleConfigVersion.cmake"
    DESTINATION lib/cmake/Bibble
)