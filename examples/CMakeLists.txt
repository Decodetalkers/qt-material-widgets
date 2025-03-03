cmake_minimum_required(VERSION 3.5)

project(
  examples
  VERSION 0.1
  LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)

file(GLOB HEADER "*.h")
file(GLOB RSOURCE "*.cpp")
file(GLOB UI "*.ui")

set(RCC_FILES examples.qrc)

add_executable(${PROJECT_NAME} ${HEADER} ${RSOURCE} ${UI} ${RCC_FILES})
target_include_directories(${PROJECT_NAME} PUBLIC ../include/qmetarial/)

target_link_libraries(
  ${PROJECT_NAME} PRIVATE Qt${QT_VERSION_MAJOR}::Widgets
                          Qt${QT_VERSION_MAJOR}::Core components)

set_target_properties(
  ${PROJECT_NAME}
  PROPERTIES MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
             MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
             MACOSX_BUNDLE_SHORT_VERSION_STRING
             ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
             MACOSX_BUNDLE TRUE)
