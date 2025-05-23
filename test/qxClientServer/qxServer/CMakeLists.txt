cmake_minimum_required(VERSION 3.15)

project(qxServer LANGUAGES CXX)

include(../../../QxOrm.cmake)

if(_QX_ENABLE_QT_NETWORK)

find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core Sql Gui Widgets REQUIRED)

set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_DEBUG_POSTFIX "d")

set(HEADERS
    ./include/precompiled.h
    ./include/export.h
    ./include/main_dlg.h
   )

set(SRCS
    ./src/main_dlg.cpp
    ./src/main.cpp
   )

set(UIS
    ./qt/ui/qxServer.ui
   )

set(QRCS
    ./qt/rcc/_qxServer.qrc
   )

if(COMMAND qt_wrap_ui)
qt_wrap_ui(UIS_HDRS ${UIS})
qt_add_resources(QRCS_HDRS ${QRCS})
else() # (COMMAND qt_wrap_ui)
qt5_wrap_ui(UIS_HDRS ${UIS})
qt5_add_resources(QRCS_HDRS ${QRCS})
endif() # (COMMAND qt_wrap_ui)

add_executable(qxServer ${SRCS} ${HEADERS} ${UIS_HDRS} ${QRCS_HDRS})

target_compile_definitions(qxServer PRIVATE -D_BUILDING_QX_SERVER)

if(COMMAND target_precompile_headers)
   target_precompile_headers(qxServer PRIVATE ./include/precompiled.h)
endif() # (COMMAND target_precompile_headers)

target_link_libraries(qxServer ${QX_LIBRARIES} Qt${QT_VERSION_MAJOR}::Gui Qt${QT_VERSION_MAJOR}::Widgets QxOrm qxServiceServer)

set_target_properties(qxServer PROPERTIES
                      ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../_bin"
                     )

set_target_properties(qxServer PROPERTIES DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX})

else() # _QX_ENABLE_QT_NETWORK

message(STATUS "qxServer project not loaded because _QX_ENABLE_QT_NETWORK option not enabled (QxOrm QxService module is disabled)")

endif() # _QX_ENABLE_QT_NETWORK
