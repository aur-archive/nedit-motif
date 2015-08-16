# Contributor: Ecmel Ercan <ecmel dot ercan at gmail dot com>
# Contributor: Eric Bélanger <eric@archlinux.org>
# Maintainer: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=nedit-motif
pkgver=5.5
pkgrel=3
pkgdesc="A Unix text editor for programmers and general users"
dirname=nedit
arch=('i686' 'x86_64')
url="http://www.nedit.org/"
license=('GPL' 'custom')
depends=('openmotif' 'libxpm')
source=("http://sourceforge.net/projects/nedit/files/nedit-source/5.5/nedit-5.5-src.tar.bz2" "nedit_xorg_composite_fix.patch")
md5sums=('48cb3dce52d44988f3a4d7c6f47b6bbe'
         'b7f4b0710bf83422c8946d0b73c0531a')
LANG=C
prepare() {
  cd "${srcdir}/${dirname}-${pkgver}"
  patch -p1 < $srcdir/nedit_xorg_composite_fix.patch
  sed -i 's/-Wl,-Bstatic//' makefiles/Makefile.linux
  sed -i 's|fgets|//fgets|' util/check_lin_tif.c
  sed -i "s/CFLAGS=-O/CFLAGS=${CFLAGS} -DBUILD_UNTESTED_NEDIT/" makefiles/Makefile.linux
  sed -i 's|"/bin/csh"|"/bin/sh"|' source/preferences.c
}

build() {
  cd "${srcdir}/${dirname}-${pkgver}"
  make linux docs
}

package() {
  cd "${srcdir}/${dirname}-${pkgver}"

  install -Dm755 source/nedit "${pkgdir}/usr/bin/nedit"
  install -Dm755 source/nc "${pkgdir}/usr/bin/nedit-client"
  install -Dm644 doc/nedit.man "${pkgdir}/usr/share/man/man1/nedit.1"
  install -Dm644 doc/nc.man "${pkgdir}/usr/share/man/man1/nedit-client.1"
  install -Dm644 doc/nedit.html "${pkgdir}/usr/share/doc/nedit/nedit.html"
  install -Dm644 README "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

