CMAKE_MINIMUM_REQUIRED( VERSION 2.8.9 )
PROJECT( EtherCurve )

IF( CMAKE_COMPILER_IS_GNUCXX )
  SET( CMAKE_CXX_FLAGS "-Werror -Wall -pedantic -std=c++0x" )
ENDIF()

SET( CMAKE_MODULE_PATH
  ${CMAKE_MODULE_PATH}
  ${CMAKE_SOURCE_DIR}
)

SET( CMAKE_AUTOMOC ON )

FIND_PACKAGE( Qt5Widgets REQUIRED )
FIND_PACKAGE( PCAP REQUIRED )

SET( SOURCES
  DeviceList.cpp
  EtherCurve.cpp
  MainWindow.cpp
  PacketRenderer.cpp
  PCAPWrapper.cpp
)

ADD_EXECUTABLE( ethercurve ${SOURCES} )

QT5_USE_MODULES( ethercurve Core )
QT5_USE_MODULES( ethercurve Gui )
QT5_USE_MODULES( ethercurve Widgets )

TARGET_LINK_LIBRARIES(
  ethercurve
  ${PCAP_LIBRARIES}
)

IF( NOT CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_CURRENT_BINARY_DIR )

  SET( RESOURCE_FILES
    Qualitative1.csv
    Qualitative2.csv
  )

  FILE(
    COPY        ${RESOURCE_FILES}
    DESTINATION ${CMAKE_CURRENT_BINARY_DIR}
  )

  MESSAGE( STATUS "Resource files setup done" )
ENDIF()
