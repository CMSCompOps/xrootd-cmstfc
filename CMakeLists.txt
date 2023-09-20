cmake_minimum_required( VERSION 3.1 )
project( xrootd-cmstfc )

set( CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake )

find_package( Xrootd REQUIRED )
find_package( XercesC REQUIRED )
find_package( Pcre REQUIRED )
find_package( Jsoncpp REQUIRED )

set (CMAKE_CXX_STANDARD 11)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall" )

include_directories( "${PROJECT_SOURCE_DIR}" "${XROOTD_INCLUDES}" "${XERCES_INCLUDES}" "${PCRE_INCLUDES}" "${JSONCPP_INCLUDES}")

add_library( XrdCmsTfc MODULE src/xml/XrdCmsTfc.cc src/xml/XrdCmsTfc.hh )
add_library( XrdCmsJson MODULE src/json/XrdCmsJson.cc src/json/XrdCmsJson.hh )

target_link_libraries(XrdCmsTfc ${XROOTD_UTILS} ${XERCES_LIB} ${PCRE_LIB})
target_link_libraries(XrdCmsJson ${XROOTD_UTILS} ${JSONCPP_LIBRARIES})


if(BUILD_TEST)
  add_executable(test_xml.o  src/xml/XrdCmsTfc.cc src/xml/XrdCmsTfc.hh tests/test_xml.cc)
  target_link_libraries(test_xml.o ${XROOTD_UTILS} ${XERCES_LIB} ${PCRE_LIB})

  add_executable(test_json.o  src/json/XrdCmsJson.cc src/json/XrdCmsJson.hh tests/test_json.cc)
  target_link_libraries(test_json.o ${XROOTD_UTILS} ${JSONCPP_LIBRARIES})

endif()

if (NOT DEFINED CMAKE_INSTALL_LIBDIR)
  SET(CMAKE_INSTALL_LIBDIR "lib64")
endif()

install(
  TARGETS XrdCmsTfc
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} )

install(
  TARGETS XrdCmsJson
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} )

install(
  FILES ${CMAKE_SOURCE_DIR}/src/xml/XrdCmsTfc.hh
  DESTINATION include )

install(
  FILES ${CMAKE_SOURCE_DIR}/src/json/XrdCmsJson.hh
  DESTINATION include )

set_target_properties(
  XrdCmsTfc
  PROPERTIES
  VERSION   "0.0.1"
  SOVERSION "0"
  LINK_INTERFACE_LIBRARIES "" )

set_target_properties(
  XrdCmsJson
  PROPERTIES
  VERSION   "0.0.1"
  SOVERSION "0"
  LINK_INTERFACE_LIBRARIES "" )


