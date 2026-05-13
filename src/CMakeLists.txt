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
    ${res}
)
target_include_directories(clipgrab PRIVATE
    .
)
