cmake_minimum_required(VERSION 2.8)
project(fwknop-gui CXX C)

set(CMAKE_OSX_ARCHITECTURES i386)

if(NOT(DEFINED IS_WIN32 OR DEFINED IS_LINUX OR DEFINED IS_APPLE))
  if(WIN32)
    set(IS_WIN32 TRUE)
  elseif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(IS_APPLE TRUE)
  else()
    set(IS_LINUX TRUE)
  endif()
endif()

if (IS_WIN32)
  set(SRCS ${SRCS} minimal.rc)
  set( wxWidgets_USE_STATIC ON)
endif()
find_package(wxWidgets 2.8.10 REQUIRED xml html adv qa richtext net core base)

include(${wxWidgets_USE_FILE})
include_directories(${CMAKE_SOURCE_DIR})

set(CODE_FILES
  configs.cpp
  fwknop_guiApp.cpp
  fwknop_guiMain.cpp
  )

add_executable(fwknop-gui WIN32 MACOSX_BUNDLE
  ${CODE_FILES}
  )

# This assumes libfko is installed and devel packages in the standard location.
# That really should have a proper library check.
target_link_libraries(fwknop-gui ${wxWidgets_LIBRARIES} fko)
if(IS_WIN32)
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static-libgcc -static-libstdc++ -static")
endif()