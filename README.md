# CoolReader3 Testing branch for Boyue Devices
Hopefully to make Eink and frontlight work on Boyue Mimas and Mars with Rockchip RK3368 chips



CoolReader 3 - cross platform open source e-book reader
=======================================================

(c) Vadim Lopatin, 1998-2018


LICENSE: All source codes (except thirdparty directory) 
are provided under the terms of GNU GPL license, version 2



Directories
-----------

        crengine   - CREngine (DOM/XML/CSS ebook rendering library) sources
        cr3gui     - CR3 with CR3GUI for e-ink devices sources
        cr3qt      - CR3 with Qt based GUI
        cr3wx      - CR3 with wxWidgets based GUI
        thirdparty - third party libraries, to use if not found in system (zlib, libpng, libjpeg, freetype, harfbuzz)
        tinydict   - small library for .dict file format support
        tools      - miscellaneous configuration files
        android    - Android port


Android Build Instructions
--------------------------

Use Android Studio - open subdirectory "android" as Android Studio project

Ensure that you have Android SDK and NDK installed



CMake Build Instructions
------------------------

        # Building QT version
        # libqt4-dev should be installed
        mkdir qtbuild
        cd qtbuild
        cmake -D GUI=QT -D CMAKE_BUILD_TYPE=Release -D MAX_IMAGE_SCALE_MUL=2 -D DOC_DATA_COMPRESSION_LEVEL=3 -D DOC_BUFFER_SIZE=0x1400000 -D CMAKE_INSTALL_PREFIX=/usr ..
        make
        sudo make install


        # Building QT version, in DEBUG mode
        mkdir qtbuild
        cd qtbuild
        cmake -D GUI=QT -D CMAKE_BUILD_TYPE=Debug -D MAX_IMAGE_SCALE_MUL=2 -D DOC_DATA_COMPRESSION_LEVEL=3 -D DOC_BUFFER_SIZE=0x1400000 -D CMAKE_INSTALL_PREFIX=/usr ..
        make
        sudo make install

        # Building QT version, in DEBUG mode, ANTIWORD development
        mkdir qtbuild
        cd qtbuild
        cmake -D GUI=QT -D CMAKE_BUILD_TYPE=Debug -D ENABLE_ANTIWORD=1 -D MAX_IMAGE_SCALE_MUL=2 -D DOC_DATA_COMPRESSION_LEVEL=3 -D DOC_BUFFER_SIZE=0x1400000 -D CMAKE_INSTALL_PREFIX=/usr ..
        make
        sudo make install

        # Building wxWidgets version
        # libwxgtk2.8-dev should be installed
        mkdir wxbuild
        cd wxbuild
        cmake -D GUI=WX -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr ..
        make

        # Building ARM version on OpenInkpot:
        mkdir armbuild
        cd armbuild
        cmake -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-oi.cmake -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Release -D GUI=CRGUI_XCB -D USE_EXTERNAL_EDICT_DICTIONARY=1 ..
        make

        # Building i386 version, Qt backend V3 simulation:
        mkdir qt-v3
        cd qt-v3
        cmake -D DEVICE_NAME=v3 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Debug -D USE_STATIC_ZLIB=1 -Wdev -D ENABLE_ANTIWORD=1 -D CMAKE_INSTALL_PREFIX=dest -D GUI=CRGUI_QT -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x500000 ..
        make

        # Building i386 version (for OpenInkpot), V3 simulation:
        mkdir xcb-v3
        cd xcb-v3
        cmake -D DEVICE_NAME=v3 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Debug -D USE_STATIC_ZLIB=1 -Wdev -D ENABLE_ANTIWORD=1 -D CMAKE_INSTALL_PREFIX=/usr -D GUI=CRGUI_XCB -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x500000 ..
        make

        # Building i386 version (for OpenInkpot), n516/azbooka simulation:
        mkdir xcb-n516
        cd xcb-n516
        cmake -D DEVICE_NAME=n516 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Debug  -D CMAKE_INSTALL_PREFIX=/usr -D GUI=CRGUI_XCB ..
        make

        # Building Jinke/LBook V3 viewer plugin (libfb2.so):
        mkdir v3build
        cd v3build
        mkdir dest
        cmake -D DEVICE_NAME=v3 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-v3.cmake -D GUI=CRGUI_JINKE_PLUGIN -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest ..
        make

        # Building Jinke/LBook V3 viewer plugin (libfb2.so), new SDK:
        mkdir v3build
        cd v3build
        mkdir dest
        cmake -D DEVICE_NAME=v3 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-linux-gnueabi.cmake -D GUI=CRGUI_JINKE_PLUGIN -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest ..
        make

        # Building Jinke/LBook V3 fb2props plugin for Bookshelf (libfb2props.so) i386:
        mkdir fb2props386
        cd fb2props386
        mkdir dest
        cmake -D GUI=FB2PROPS -D CMAKE_BUILD_TYPE=Debug -D CMAKE_INSTALL_PREFIX=dest ..
        make

        # Building Jinke/LBook V3 fb2props plugin for Bookshelf (libfb2props.so):
        mkdir v3fb2propsbuild
        cd v3fb2propsbuild
        mkdir dest
        cmake -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-v3.cmake -D GUI=FB2PROPS -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest ..
        make

        # Building Jinke/LBook V3 fb2props plugin for Bookshelf NEW SDK (libfb2props.so):
        mkdir v3newfb2propsbuild
        cd v3newfb2propsbuild
        mkdir dest
        cmake -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-linux-gnueabi.cmake -D GUI=FB2PROPS -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest ..
        make

        # Building Jinke/LBook V3 new SDK viewer app (cr3):
        mkdir v3app
        cd v3app
        #cmake -D DEVICE_NAME=v3 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-linux-gnueabi.cmake -D MAX_IMAGE_SCALE_MUL=2 -D GUI=CRGUI_NANOX -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x500000 -D BIG_PAGE_MARGINS=1 ..
        cmake -D DEVICE_NAME=v3 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-linux-gnueabi.cmake -D MAX_IMAGE_SCALE_MUL=2 -D GUI=CRGUI_NANOX -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x500000 ..
        make

        # Building Jinke/LBook V5 viewer app (cr3):
        mkdir v5build
        cd v5build
        cmake -D DEVICE_NAME=v5 -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-v5.cmake -D GUI=CRGUI_NANOX -D GRAY_BACKBUFFER_BITS=3 -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x580000 ..
        #cmake -D DEVICE_NAME=v5 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-v5.cmake -D GUI=CRGUI_NANOX -D GRAY_BACKBUFFER_BITS=3 -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest ..

        make

        # Building Jinke/LBook V3+ viewer app (cr3):
        mkdir v3abuild
        cd v3abuild
        cmake -D DEVICE_NAME=v3a -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-v5.cmake -D GUI=CRGUI_NANOX -D CR3_PNG=1 -D CR3_JPEG=1 -D CR3_FREETYPE=1 -D GRAY_BACKBUFFER_BITS=4 -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest -D RAM_COMPRESSED_BUFFER_ENABLED=0 -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x1000000 ..
        make

        # Building ARM version for PocketBook:
        mkdir pb360
        cd pb360
        cmake -D DEVICE_NAME=pb360 -D CMAKE_INSTALL_PREFIX=/usr/local/pocketbook/mnt/ext1 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-pocketbook.cmake -D CMAKE_CXX_FLAGS_RELEASE:STRING="-fomit-frame-pointer -O1" -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Release -D GUI=CRGUI_PB -D ENABLE_CHM=1 -D ENABLE_ANTIWORD=1 ..
        make

        # Building ARM version for PocketBook Pro
        mkdir pbPro
        cd pbPro
        cmake -D DEVICE_NAME=pb360 -D CMAKE_INSTALL_PREFIX=/usr/local/pocketbook/mnt/ext1 -D CMAKE_TOOLCHAIN_FILE=../tools/toolchain-arm-gnu-eabi-pocketbook.cmake -D MAX_IMAGE_SCALE_MUL=2 -D CMAKE_BUILD_TYPE=Release -D ENABLE_CHM=1 -D ENABLE_ANTIWORD=1 -D GUI=CRGUI_PB -D POCKETBOOK_PRO=1 ..

        # Building Jinke/LBook V3+ simulator for Win32 (cr3):
        mkdir v3win32
        cd v3win32
        cmake -D DEVICE_NAME=v3a -G "Visual Studio 10" -D MAX_IMAGE_SCALE_MUL=2 -D GUI=CRGUI_WIN32 -D GRAY_BACKBUFFER_BITS=4 -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=dest -D DOC_DATA_COMPRESSION_LEVEL=1 -D DOC_BUFFER_SIZE=0x800000 ..
        make


