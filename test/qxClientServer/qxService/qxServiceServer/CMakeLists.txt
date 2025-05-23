cmake_minimum_required(VERSION 3.15)

project(qxServiceServer LANGUAGES CXX)

include(../../../../QxOrm.cmake)

if(_QX_ENABLE_QT_NETWORK)

set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_DEBUG_POSTFIX "d")

set(HEADERS
    ../include/precompiled.h
    ../include/export.h
    ../include/service/server_infos.h
    ../include/service/user_service.h
    ../include/business_object/user.h
    ../include/business_object/user_search.h
    ../include/dao/user_manager.h
   )

set(SRCS
    ../src/service/server_infos.cpp
    ../src/service/user_service.cpp
    ../src/business_object/user.cpp
    ../src/business_object/user_search.cpp
    ../src/dao/user_manager.cpp
    ../src/main.cpp
   )

add_library(qxServiceServer SHARED ${SRCS} ${HEADERS})

target_compile_definitions(qxServiceServer PRIVATE -D_BUILDING_QX_SERVICE)

if(COMMAND target_precompile_headers)
   target_precompile_headers(qxServiceServer PRIVATE ../include/precompiled.h)
endif() # (COMMAND target_precompile_headers)

target_link_libraries(qxServiceServer ${QX_LIBRARIES} QxOrm)

set_target_properties(qxServiceServer PROPERTIES
                      ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_MINSIZEREL "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      LIBRARY_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                      RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO "${CMAKE_CURRENT_SOURCE_DIR}/../../../_bin"
                     )

else() # _QX_ENABLE_QT_NETWORK

message(STATUS "qxServiceServer project not loaded because _QX_ENABLE_QT_NETWORK option not enabled (QxOrm QxService module is disabled)")

endif() # _QX_ENABLE_QT_NETWORK
