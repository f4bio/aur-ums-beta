# Maintainer: Red Squirrel <iam at redsquirrel87 dot com>
# Based on PMS PKGBUILD

pkgname=ums
pkgver=6.3.1
pkgdate=1463738429
pkgrel=1
pkgdesc="Universal Media Server: a DLNA-compliant UPnP Media Server. Build based on Java 8."
arch=('i686' 'x86_64')
url="http://www.universalmediaserver.com/"
license=('GPL2')
depends=('mplayer' 'ffmpeg' 'mencoder' 'libmediainfo' 'java-runtime=8' 'tsmuxer-cli-ng')
makedepends=("unzip")
[ "$CARCH" = "i686" ] && \
optdepends=("vlc: For Internet video/audio")
[ "$CARCH" = "x86_64" ] && \
optdepends=("vlc: Internet video/audio support"
            "dcraw: thumbnails creation support"
            "lib32-gcc-libs: tsMuxeR support"
            "lib32-glibc: tsMuxeR support")
backup=(opt/ums/UMS.conf \
        opt/ums/WEB.conf)
source=("http://app.oldfoss.com:81/download/Universal-Media-Server/$pkgdateUMS-$pkgver-Java8.tgz"
        'ums.desktop'
        'ums.service')
sha256sums=('8cb40d40b54d8da6fda7786a09588f735008acbf7e99a10a67d41a1bee26e18a'
            '0cdadbabef215b6539e56755147a8f626d9f1fadfb85e2e5b7f7f1b66f1cdef9'
            'e9709c58a909b79062604425e18e0ab7a8ee5d7b823fb481dcc9269b02fcc4a7')

package() {
  mkdir -p $pkgdir/opt/ums
  mkdir $pkgdir/opt/ums/database
  mkdir -p $pkgdir/usr/bin
  chmod -R 755 $srcdir/ums-$pkgver/plugins $srcdir/ums-$pkgver/documentation
  rm -R $srcdir/ums-$pkgver/linux/*
  cp -r $srcdir/ums-$pkgver/* $pkgdir/opt/ums/
  ln -s /usr/bin/ffmpeg $pkgdir/opt/ums/linux/ffmpeg
  ln -s /usr/bin/ffmpeg $pkgdir/opt/ums/linux/ffmpeg64
  ln -s /usr/bin/tsMuxeR $pkgdir/opt/ums/linux/tsMuxeR
  ln -s /usr/bin/tsMuxeR $pkgdir/opt/ums/linux/tsMuxeR-new
  chmod +x $pkgdir/opt/ums/UMS.sh
  touch $pkgdir/opt/ums/UMS.conf
  touch $pkgdir/opt/ums/debug.log
  chgrp users $pkgdir/opt/ums/UMS.conf \
              $pkgdir/opt/ums/WEB.conf \
              $pkgdir/opt/ums/debug.log \
              $pkgdir/opt/ums/database

  chmod g+w $pkgdir/opt/ums/UMS.conf \
            $pkgdir/opt/ums/WEB.conf \
            $pkgdir/opt/ums/debug.log \
            $pkgdir/opt/ums/database 

  unzip -q -u $srcdir/ums-$pkgver/ums.jar -d ums_jar
  install -d -m 755 $pkgdir/usr/share/pixmaps
  install -D -m 644 $srcdir/ums_jar/resources/images/logo.png $pkgdir/usr/share/pixmaps/ums.png
  install -D -m 644 $srcdir/ums.desktop $pkgdir/usr/share/applications/ums.desktop
  install -D -m 644 $srcdir/ums.service $pkgdir/usr/lib/systemd/system/ums@.service
}
