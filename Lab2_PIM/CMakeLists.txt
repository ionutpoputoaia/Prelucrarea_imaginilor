cmake_minimum_required(VERSION 3.16)
project(Lab2_PIM VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Activează generarea automată pentru MOC, UIC și RCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)


# Caută direct Qt6 (renunțăm la "NAMES QT" care dădea eroare)
find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)

# Restul fișierelor tale...
set(PROJECT_SOURCES
    AbstractViewer.cpp
    HistogramViewer.cpp
    ImageGrid.cpp
    ImageGridCell.cpp
    ImageViewer.cpp
    Lab2_PIM.cpp
    Tools.cpp
    AbstractViewer.h
    HistogramViewer.h
    ImageGrid.h
    ImageGridCell.h
    ImageViewer.h
    operatii.h
    PITimer.h
    resource.h
    Tools.h
    Lab2_PIM.ui
    Lab2_PIM.qrc
)

add_executable(Lab2_PIM ${PROJECT_SOURCES})

# Leagă modulele Qt6
target_link_libraries(Lab2_PIM PRIVATE
    Qt6::Core
    Qt6::Gui
    Qt6::Widgets
)

# Copiază automat folderul Images lângă executabil
add_custom_command(TARGET Lab2_PIM POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_CURRENT_SOURCE_DIR}/Images"
        "$<TARGET_FILE_DIR:Lab2_PIM>/Images"
    COMMENT "Se copiaza folderul Images langa executabil..."
)