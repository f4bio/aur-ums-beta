# Maintainer: Mitch <mitch at znation dot nl>
# Contributor: Red Squirrel <iam at redsquirrel87 dot com>
# Based on PMS PKGBUILD

pkgname=ums-beta
pkgver=7.0.0-rc2
pkgrel=1
pkgdesc="Universal Media Server: a DLNA-compliant UPnP Media Server. Build based on Java 8."
arch=('i686' 'x86_64')
url="http://www.universalmediaserver.com/"
license=('GPL2')
depends=('mplayer' 'ffmpeg' 'mencoder' 'libmediainfo' 'java-runtime=8' 'tsmuxer-ng-cli-bin')
makedepends=("unzip")
[ "$CARCH" = "i686" ] && \
optdepends=("vlc: For Internet video/audio")
[ "$CARCH" = "x86_64" ] && \
optdepends=("vlc: Internet video/audio support"
            "dcraw: thumbnails creation support"
            "lib32-gcc-libs: tsMuxeR support"
            "lib32-glibc: tsMuxeR support")
backup=(opt/ums-beta/UMS.conf \
        opt/ums-beta/WEB.conf)
source=("https://www.fosshub.com/Universal-Media-Server.html/UMS-$pkgver.tgz"
        'ums.desktop'
        'ums.service'
        'ums.timer')
sha256sums=('8435a4e64573cab7145488456876ad701d6585a1aaa2b2428a0d6e3c98247d53'
            'ba81592f9c295e5643b15a34134c738df37d9ac2349697ed9bc96065d595cbb3'
            'cd61840b5abc62dd88e0f9b4ebe87559a96483deb4baf86f9d4b3144c54b6da3'
            '54ffff80c88f05ea23d0f063f273bc28d3028289735d7408fc264931856218f4')

package() {
  mkdir -p ${pkgdir}/opt/ums-beta
  mkdir ${pkgdir}/opt/ums-beta/database
  mkdir -p ${pkgdir}/usr/bin
  chmod -R 755 ${srcdir}/ums-$pkgver/plugins ${srcdir}/ums-$pkgver/documentation
  rm -R ${srcdir}/ums-$pkgver/linux/*
  cp -r ${srcdir}/ums-$pkgver/* ${pkgdir}/opt/ums-beta/
  ln -s /usr/bin/ffmpeg ${pkgdir}/opt/ums-beta/linux/ffmpeg
  ln -s /usr/bin/ffmpeg ${pkgdir}/opt/ums-beta/linux/ffmpeg64
  ln -s /usr/bin/tsMuxeR ${pkgdir}/opt/ums-beta/linux/tsMuxeR
  ln -s /usr/bin/tsMuxeR ${pkgdir}/opt/ums-beta/linux/tsMuxeR-new
  chmod +x ${pkgdir}/opt/ums-beta/UMS.sh
  touch ${pkgdir}/opt/ums-beta/UMS.conf
  touch ${pkgdir}/opt/ums-beta/debug.log
  chgrp users ${pkgdir}/opt/ums-beta/UMS.conf \
              ${pkgdir}/opt/ums-beta/WEB.conf \
              ${pkgdir}/opt/ums-beta/debug.log \
              ${pkgdir}/opt/ums-beta/database

  chmod g+w ${pkgdir}/opt/ums-beta/UMS.conf \
            ${pkgdir}/opt/ums-beta/WEB.conf \
            ${pkgdir}/opt/ums-beta/debug.log \
            ${pkgdir}/opt/ums-beta/database

  unzip -q -u ${srcdir}/ums-$pkgver/ums.jar -d ums_jar
  install -d -m 755 ${pkgdir}/usr/share/pixmaps
  install -D -m 644 ${srcdir}/ums_jar/resources/images/logo.png ${pkgdir}/usr/share/pixmaps/ums.png
  install -D -m 644 ${srcdir}/ums.desktop ${pkgdir}/usr/share/applications/ums.desktop
  install -D -m 644 ${srcdir}/ums.service ${pkgdir}/usr/lib/systemd/system/ums@.service
  install -D -m 644 ${srcdir}/ums.timer ${pkgdir}/usr/lib/systemd/system/ums@.timer
}
