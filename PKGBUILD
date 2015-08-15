# Maintainer:
# Contributor: Gianmarco Brocchi <gianmarcobrocchi@gmail.com>

pkgname=clinica
pkgver=0.3.0
pkgrel=1
pkgdesc="Simple medical records manager"
arch=('i686' 'x86_64')
url="https://launchpad.net/clinica-project"
license=('GPL3')
depends=('libgee06' 'libpeas' 'jansson' 'libsoup' 'librsvg' 'yelp')
makedepends=('cmake' 'vala' 'intltool')
optdepends=('python2-gobject: for Agenzia del Farmaco plugin')
install=clinica.install
options=('!makeflags')
source=("https://launchpad.net/clinica-project/stable/${pkgver}/+download/${pkgname}-${pkgver}.tar.bz2")
md5sums=('dae10a4e10c7d148f05ae56d1b0ae47d')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  sed -i -e "s:-Werror=format-security:-Wformat -Werror=format-security:g" CMakeLists.txt
  sed -i 's@^#!.*python$@#!/usr/bin/python2@' plugins/AgenziaDelFarmaco.py
  sed -i -e "s:Application;GTK;:Office;GTK;:g" data/clinica.desktop

  mkdir build
  cd build  
  cmake \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DGSETTINGS_COMPILE=OFF \
    -DGSETTINGS_COMPILE_IN_PLACE=OFF \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_SKIP_RPATH=ON ..

  LC_ALL=C LANG=C make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}/build"

  make DESTDIR="${pkgdir}" install
}
