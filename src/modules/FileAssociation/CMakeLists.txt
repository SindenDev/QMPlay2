cmake_minimum_required(VERSION 2.8.6)
if(COMMAND cmake_policy)
    if(POLICY CMP0003)
        cmake_policy(SET CMP0003 NEW)
    endif()
    if(POLICY CMP0020)
        cmake_policy(SET CMP0020 NEW)
    endif()
    if(POLICY CMP0042)
        cmake_policy(SET CMP0042 NEW)
    endif()
    if(POLICY CMP0043)
        cmake_policy(SET CMP0043 NEW)
    endif()
endif()
project(FileAssociation)

set(FileAssociation_HDR
    FileAssociation.hpp
)

set(FileAssociation_SRC
    FileAssociation.cpp
)

set(FileAssociation_RESOURCES
    icon.qrc
)

if(USE_QT5)
    qt5_add_resources(FileAssociation_RESOURCES_RCC ${FileAssociation_RESOURCES})
else()
    qt4_add_resources(FileAssociation_RESOURCES_RCC ${FileAssociation_RESOURCES})
endif()

include_directories(../../qmplay2/headers)

add_library(${PROJECT_NAME} ${QMPLAY2_MODULE}
    ${FileAssociation_HDR}
    ${FileAssociation_SRC}
    ${FileAssociation_RESOURCES_RCC}
)

if(USE_QT5)
    qt5_use_modules(${PROJECT_NAME} Gui Widgets)
else()
    target_link_libraries(${PROJECT_NAME} Qt4::QtCore Qt4::QtGui)
endif()

add_dependencies(${PROJECT_NAME} libqmplay2)
target_link_libraries(${PROJECT_NAME}
    ${qmplay2lib}
    shlwapi
)

install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION ${MODULES_INSTALL_PATH})
