cmake_minimum_required(VERSION 3.19)
project(Busbomproject LANGUAGES CXX)

# ✅ Qt6 모듈 찾기
find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets Network LinguistTools)
find_package(Qt6 REQUIRED COMPONENTS Widgets)
find_package(Qt6 REQUIRED COMPONENTS Widgets)
find_package(Qt6 REQUIRED COMPONENTS Sql)
find_package(Qt6 REQUIRED COMPONENTS Multimedia)
find_package(Qt6 REQUIRED COMPONENTS MultimediaWidgets)
find_package(Qt6 REQUIRED COMPONENTS Network)

# ✅ OpenCV 추가
set(OpenCV_DIR "C:/opencv/build")
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

qt_standard_project_setup()

qt_add_executable(Busbomproject
    WIN32 MACOSX_BUNDLE
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    settingsdialog.h
    settingsdialog.cpp
    img.qrc
    loginpage.h loginpage.cpp
    appmanager.h appmanager.cpp
    signuppage.h signuppage.cpp
    dbmanager.h dbmanager.cpp
)

target_link_libraries(${PROJECT_NAME} PRIVATE Qt6::Sql)

qt_add_translations(
    TARGETS Busbomproject
    TS_FILES Busbomproject_ko_KR.ts
)

target_link_libraries(Busbomproject
    PRIVATE
        Qt6::Core
        Qt6::Gui
        Qt6::Widgets
        Qt6::Network
        ${OpenCV_LIBS}     # ✅ OpenCV 라이브러리 연결
        Qt6::Multimedia
        Qt6::MultimediaWidgets
)

target_link_libraries(Busbomproject PRIVATE Qt6::Widgets)
target_link_libraries(Busbomproject PRIVATE Qt6::Widgets)
target_link_libraries(Busbomproject PRIVATE Qt6::Network)

include(GNUInstallDirs)

install(TARGETS Busbomproject
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET Busbomproject
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
