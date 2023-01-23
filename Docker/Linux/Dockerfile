# syntax = docker/dockerfile:1.3

FROM ubuntu:18.04

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git \
    wget \
    xz-utils \
    build-essential \
    libfontconfig1-dev \
    libfreetype6-dev \
    libx11-dev \
    libxext-dev \
    libxfixes-dev \
    libxi-dev \
    libxrender-dev \
    libxcb1-dev \
    libx11-xcb-dev \
    libxcb-glx0-dev \
    libxkbcommon-x11-dev \
    mesa-common-dev \
    freeglut3 \
    freeglut3-dev \
    libglew1.5 \
    libglew1.5-dev \
    libglu1-mesa \
    libglu1-mesa-dev \
    libgl1-mesa-glx \
    libgl1-mesa-dev \
    python \
    chrpath \
    zlib1g-dev \
    liblzma-dev \
    libbz2-dev \
    && apt-get clean cache

RUN wget -q https://download.qt.io/archive/qt/5.15/5.15.8/single/qt-everywhere-opensource-src-5.15.8.tar.xz \
    && tar xf qt-everywhere-opensource-src-5.15.8.tar.xz \
    && rm qt-everywhere-opensource-src-5.15.8.tar.xz \
    && cd qt-everywhere-src-5.15.8 \
    && rm -rf web* qt3d qtmultimedia qtvirtualkeyboard qtscript qtremoteobjects qtlocation qtandroidextras qtcanvas3d qtcharts qtdatavis3d qtgamepad qtmacextras qtpurchasing qtscxml qtsensors qtserialbus qtserialport qtspeech qtvirtualkeyboard qtwinextras qtwebchannel qtwebengine qtwebglplugin qtwebsockets qtwebview qtwayland qtxmlpatterns qtgraphicaleffects qtconnectivity qtactiveqt qtnetworkauth qtlottie qtquick3d qtquicktimeline \
    && ./configure -opensource -nomake tests -nomake examples -no-icu -confirm-license -no-dbus -sql-sqlite \
    && make \
    && make install \
    && rm -rf qt-everywhere-src-5.15.8

ENV PATH="${PATH}:/usr/local/Qt-5.15.8/bin/"

RUN wget https://download.qt.io/official_releases/qt-installer-framework/4.5.1/installer-framework-opensource-src-4.5.1.tar.xz \
    && tar xf installer-framework-opensource-src-4.5.1.tar.xz \
    && rm installer-framework-opensource-src-4.5.1.tar.xz \
    && cd installer-framework-opensource-src-4.5 \
    && qmake \
    && make \
    && make install \
    && rm -rf installer-framework-opensource-src-4.5
