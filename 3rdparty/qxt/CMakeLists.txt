cmake_minimum_required(VERSION 2.6)

set(QXT-SOURCES
  qxtglobal.cpp
  qxtglobalshortcut.cpp
)

set(QXT-MOC-HEADERS
  qxtglobalshortcut.h
)

if (NOT WIN32 AND NOT APPLE)
  find_package(X11)
  include_directories(${X11_INCLUDE_DIR})
endif (NOT WIN32 AND NOT APPLE)

include_directories( ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR} ${QTINCLUDES} )

if(WIN32)
  set(QXT-SOURCES ${QXT-SOURCES} qxtglobalshortcut_win.cpp)
elseif(APPLE)
  set(QXT-SOURCES ${QXT-SOURCES} qxtglobalshortcut_mac.cpp)
else(WIN32)
  set(QXT-SOURCES ${QXT-SOURCES} qxtglobalshortcut_x11.cpp)
endif(WIN32)

if (ENABLE_QT5)
    QT5_WRAP_CPP(QXT-SOURCES-MOC ${QXT-MOC-HEADERS})
else (ENABLE_QT5)
    QT4_WRAP_CPP(QXT-SOURCES-MOC ${QXT-MOC-HEADERS})
endif (ENABLE_QT5)

ADD_LIBRARY(qxt STATIC
  ${QXT-SOURCES}
  ${QXT-SOURCES-MOC}
)
