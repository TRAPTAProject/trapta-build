This docker image is based on raspian/stretch.
It includes Qt LTS 5.12.9

To build this image, install docker on your machine, then in a terminal:

$ docker build -t raspian_qt:1.0 .

Once built, the image is kept in the docker storage space, but you can save the image:
$ docker save raspian_qt:1.0 | gzip > raspian_qt.tar.gz
Later, you can load it like this:
$ docker load < raspian_qt.tar.gz

Qt5.12.9 is located in /usr/local/Qt5.12.9

To compile traptaviewer with this docker image, go to /home:

$ cd /home
$ git clone https://github.com/TRAPTAProject/traptaviewer.git
$ cd traptaviewer
$ /usr/local/Qt-5.12.9/bin/qmake
$ make

$ readelf -d ./TRAPTAViewer

Dynamic section at offset 0x65eb4 contains 36 entries:
  Tag        Type                         Name/Value
 0x00000001 (NEEDED)                     Shared library: [libQt5Quick.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Gui.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Qml.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Network.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Core.so.5]
 0x00000001 (NEEDED)                     Shared library: [libbrcmGLESv2.so]
 0x00000001 (NEEDED)                     Shared library: [libbrcmEGL.so]
 0x00000001 (NEEDED)                     Shared library: [libpthread.so.0]
 0x00000001 (NEEDED)                     Shared library: [libstdc++.so.6]
 0x00000001 (NEEDED)                     Shared library: [libm.so.6]
 0x00000001 (NEEDED)                     Shared library: [libgcc_s.so.1]
 0x00000001 (NEEDED)                     Shared library: [libc.so.6]
 0x0000000f (RPATH)                      Library rpath: [/usr/local/Qt-5.12.9/lib]


Change the library rpath in the executable file:

$ chrpath -r ./lib/ ./TRAPTAViewer

./TRAPTAViewer: RPATH=/usr/local/Qt-5.12.9/lib
./TRAPTAViewer: new RPATH: ./lib/

$ readelf -d ./TRAPTAViewer

Dynamic section at offset 0x65eb4 contains 36 entries:
  Tag        Type                         Name/Value
 0x00000001 (NEEDED)                     Shared library: [libQt5Quick.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Gui.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Qml.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Network.so.5]
 0x00000001 (NEEDED)                     Shared library: [libQt5Core.so.5]
 0x00000001 (NEEDED)                     Shared library: [libbrcmGLESv2.so]
 0x00000001 (NEEDED)                     Shared library: [libbrcmEGL.so]
 0x00000001 (NEEDED)                     Shared library: [libpthread.so.0]
 0x00000001 (NEEDED)                     Shared library: [libstdc++.so.6]
 0x00000001 (NEEDED)                     Shared library: [libm.so.6]
 0x00000001 (NEEDED)                     Shared library: [libgcc_s.so.1]
 0x00000001 (NEEDED)                     Shared library: [libc.so.6]
 0x0000000f (RPATH)                      Library rpath: [./lib/]

