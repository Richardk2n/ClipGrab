cmake_minimum_required(VERSION 3.16)
project(clipgrab VERSION 3.9.14 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt6 REQUIRED COMPONENTS Core5Compat Gui LinguistTools Network WebEngineWidgets Widgets Xml)

qt_standard_project_setup(I18N_TRANSLATED_LANGUAGES bg bn ca cs de el es eu fa fi fr hr hu id it ja ko lt mk nl no pa pl pt ro ru si sr strings sv sw tr vi zh)

add_subdirectory(src)

target_compile_definitions(clipgrab PRIVATE
    CLIPGRAB_VERSION=3.9.14
)

target_link_libraries(clipgrab PRIVATE
    Qt::Core
    Qt::Core5Compat
    Qt::Gui
    Qt::Network
    Qt::WebEngineWidgets
    Qt::Widgets
    Qt::Xml
)


# Resources:

qt_add_translations(TARGETS clipgrab TS_OUTPUT_DIRECTORY i18n RESOURCE_PREFIX lng)
set(resources2_resource_files
    "mozilla-root-cas.txt"
)

qt_add_resources(clipgrab "resources2"
    PREFIX
        "/crt"
    FILES
        ${resources2_resource_files}
)
set(resources3_resource_files
    "loading-failed.html"
    "loading-progress.html"
    "loading-styles.css"
    "search-styles.css"
)

qt_add_resources(clipgrab "resources3"
    PREFIX
        "/search"
    FILES
        ${resources3_resource_files}
)

if(MACOS)
    target_link_libraries(clipgrab PRIVATE
        "-framework AppKit"
        "-framework Foundation"
    )
endif()

install(TARGETS clipgrab
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET clipgrab
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
