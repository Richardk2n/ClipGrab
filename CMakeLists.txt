cmake_minimum_required(VERSION 3.16)
project(clipgrab VERSION 3.9.14 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt6 REQUIRED COMPONENTS Core5Compat Gui Network WebEngineWidgets Widgets Xml)

qt_standard_project_setup()

qt_add_executable(clipgrab WIN32 MACOSX_BUNDLE
    clipgrab.cpp clipgrab.h
    converter.cpp converter.h
    converter_copy.cpp converter_copy.h
    converter_ffmpeg.cpp converter_ffmpeg.h
    download_list_model.cpp download_list_model.h
    helper_downloader.cpp helper_downloader.h helper_downloader.ui
    main.cpp
    mainwindow.cpp mainwindow.h mainwindow.ui
    message_dialog.cpp message_dialog.h message_dialog.ui
    metadata-dialog.ui
    notifications.cpp notifications.h
    update_message.ui
    video.cpp video.h
    web_engine_view.cpp web_engine_view.h
    youtube_dl.cpp youtube_dl.h
)
target_include_directories(clipgrab PRIVATE
    .
)

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
set(resources_resource_files
    "icon.png"
    "logo.png"
    "paypal-logo.png"
    "splash.png"
)

qt_add_resources(clipgrab "resources"
    PREFIX
        "/img"
    FILES
        ${resources_resource_files}
)
set(resources1_resource_files
    "clipgrab_bg.qm"
    "clipgrab_bn.qm"
    "clipgrab_ca.qm"
    "clipgrab_cs.qm"
    "clipgrab_de.qm"
    "clipgrab_el.qm"
    "clipgrab_es.qm"
    "clipgrab_eu.qm"
    "clipgrab_fa.qm"
    "clipgrab_fi.qm"
    "clipgrab_fr.qm"
    "clipgrab_hr.qm"
    "clipgrab_hu.qm"
    "clipgrab_id.qm"
    "clipgrab_it.qm"
    "clipgrab_ja.qm"
    "clipgrab_ko.qm"
    "clipgrab_lt.qm"
    "clipgrab_mk.qm"
    "clipgrab_nl.qm"
    "clipgrab_no.qm"
    "clipgrab_pa.qm"
    "clipgrab_pl.qm"
    "clipgrab_pt.qm"
    "clipgrab_ro.qm"
    "clipgrab_ru.qm"
    "clipgrab_si.qm"
    "clipgrab_sr.qm"
    "clipgrab_sv.qm"
    "clipgrab_sw.qm"
    "clipgrab_tr.qm"
    "clipgrab_vi.qm"
    "clipgrab_zh.qm"
)

qt_add_resources(clipgrab "resources1"
    PREFIX
        "/lng"
    FILES
        ${resources1_resource_files}
)
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
