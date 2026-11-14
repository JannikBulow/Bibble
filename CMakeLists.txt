cmake_minimum_required(VERSION 3.26)

if(NOT DEFINED BIBBLE_VERSION OR BIBBLE_VERSION STREQUAL "")
    message(FATAL_ERROR "BIBBLE_VERSION is required. Pass -DBIBBLE_VERSION=x.y.z")
endif()

project(Bibble VERSION "${BIBBLE_VERSION}")

set(CPACK_PACKAGE_NAME "bibble")
set(CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Bibble SDK")
set(CPACK_PACKAGE_CONTACT "jannikbulow0@gmail.com")

include(CMakePackageConfigHelpers)
include(CTest)
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

if(WIN32)
    set(CPACK_GENERATOR "NSIS")

    set(CPACK_NSIS_DISPLAY_NAME "Bibble")
    set(CPACK_PACKAGE_INSTALL_DIRECTORY "Bibble")
    set(CPACK_NSIS_ENABLE_UNINSTALL_BEFORE_INSTALL ON)
    set(CPACK_NSIS_MODIFY_PATH OFF)

    set(CPACK_NSIS_EXTRA_INSTALL_COMMANDS [=[
        EnVar::SetHKCU
        EnVar::AddValue "Path" "$INSTDIR\bin"
        Pop $0

        StrCmp $0 "0" bibble_path_done
        MessageBox MB_ICONEXCLAMATION "Could not update user PATH (EnVar error $0)."
        Abort

        bibble_path_done:
    ]=])

    set(CPACK_NSIS_EXTRA_UNINSTALL_COMMANDS [=[
        EnVar::SetHKCU
        EnVar::DeleteValue "Path" "$INSTDIR\bin"
        Pop $0
    ]=])

    set(CPACK_VERBATIM_VARIABLES ON)

elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    set(CPACK_GENERATOR "DEB")

    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Jannik Bülow")
    set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)
    set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)
endif()

set(CPACK_VERBATIM_VARIABLES ON)
include(CPack)
