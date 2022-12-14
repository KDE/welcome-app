cmake_minimum_required(VERSION 3.16)

project(welcome)

include(FeatureSummary)

set(PROJECT_VERSION "5.26.80")
set(REQUIRED_QT_VERSION 5.15)
set(KF5_MIN_VERSION 5.98)

find_package(ECM ${KF5_MIN_VERSION} REQUIRED NO_MODULE)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${ECM_MODULE_PATH})

include(KDEInstallDirs)
include(KDECMakeSettings)
include(KDECompilerSettings NO_POLICY_SCOPE)
include(ECMSetupVersion)
include(ECMGenerateHeaders)
include(ECMPoQmTools)

ecm_setup_version(${PROJECT_VERSION}
    VARIABLE_PREFIX PLASMA_WELCOME
    VERSION_HEADER "${CMAKE_CURRENT_BINARY_DIR}/src/plasma-welcome-version.h"
)

find_package(Qt${QT_MAJOR_VERSION} ${REQUIRED_QT_VERSION} REQUIRED COMPONENTS Core Gui Qml QuickControls2 Svg)
find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS Kirigami2 CoreAddons DBusAddons Declarative I18n KIO NetworkManagerQt Notifications Plasma Service WindowSystem)

add_subdirectory(src)

install(PROGRAMS org.kde.plasma-welcome.desktop DESTINATION ${KDE_INSTALL_APPDIR})
install(FILES org.kde.plasma-welcome.appdata.xml DESTINATION ${KDE_INSTALL_METAINFODIR})

feature_summary(WHAT ALL INCLUDE_QUIET_PACKAGES FATAL_ON_MISSING_REQUIRED_PACKAGES)
