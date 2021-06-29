FROM raspbian/stretch

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    python \
    git \
    libfontconfig1-dev \
    libdbus-1-dev \
    libfreetype6-dev \
    libicu-dev \
    libinput-dev \
    libxkbcommon-dev \
    libsqlite3-dev \
    libssl-dev \
    libpng-dev \
    libjpeg-dev \
    libglib2.0-dev \
    libraspberrypi-dev \
    chrpath

RUN cd /home \
    && wget https://download.qt.io/archive/qt/5.12/5.12.9/single/qt-everywhere-src-5.12.9.tar.xz \
    && tar xf qt-everywhere-src-5.12.9.tar.xz \
    && rm qt-everywhere-src-5.12.9.tar.xz \
    && git clone https://github.com/oniongarlic/qt-raspberrypi-configuration.git \ 
    && cd qt-raspberrypi-configuration \
    && make install DESTDIR=../qt-everywhere-src-5.12.9 \
    && cd .. \
    && cd qt-everywhere-src-5.12.9 \
    && rm -rf web* qt3d qtmultimedia qtvirtualkeyboard qtscript qtremoteobjects qtlocation qtandroidextras qtcanvas3d qtcharts qtdatavis3d qtgamepad qtmacextras qtpurchasing qtscxml qtsensors qtserialbus qtserialport qtspeech qtvirtualkeyboard qtwinextras qtwebchannel qtwebengine qtwebglplugin qtwebsockets qtwebview qtwayland qtxmlpatterns qtgraphicaleffects qtconnectivity qtactiveqt qtnetworkauth qttools qtlottie qtquick3d qtquicktimeline \
    && PKG_CONFIG_LIBDIR=/usr/lib/arm-linux-gnueabihf/pkgconfig:/usr/share/pkgconfig ./configure -platform linux-rpi3-g++ -v -opengl es2 -eglfs -qpa eglfs -no-gtk -opensource -confirm-license -release -reduce-exports -force-pkg-config -nomake examples -no-compile-examples -qt-pcre -no-pch -no-xcb -no-icu -no-dbus -no-cups -no-tslib -sql-sqlite -no-openssl -evdev -system-freetype -fontconfig -glib \
    && make \
    && make install \
    && cd .. \
    && rm -rf qt-everywhere-src-5.12.9 \
    && rm -rf qt-raspberrypi-configuration

