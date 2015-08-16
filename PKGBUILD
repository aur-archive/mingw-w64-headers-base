# Maintainer: rubenvb vanboxem <dottie> ruben <attie> gmail <dottie> com
pkgname=mingw-w64-headers-base
pkgver=2.0.1
pkgrel=1
pkgdesc="MinGW-w64 headers for Windows (bootstrap)"
arch=('any')
url="http://mingw-w64.sourceforge.net"
license=('custom')
groups=('mingw-w64-bootstrap' 'mingw-w64')
depends=()
makedepends=()
optdepends=()
provides=('mingw-w64-headers-bootstrap')
conflicts=('mingw-w64-headers' 'mingw-w64-winpthreads')
replaces=()
backup=()
options=('!strip' '!libtool' '!emptydirs')
source=(http://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/mingw-w64-v${pkgver}.tar.gz)
md5sums=('ebb650e66f18f242676a53e0de05f3a9')

_targets="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  for _target in ${_targets}; do
    msg "Configuring ${_target} headers"
    mkdir -p ${srcdir}/headers-${_target} && cd ${srcdir}/headers-${_target}
    ${srcdir}/mingw-w64-v${pkgver}/mingw-w64-headers/configure --prefix=/usr --enable-sdk=all --host=${_target}
  done
}

package() {
  for _target in ${_targets}; do
    msg "Installing ${_target} headers"
    cd ${srcdir}/headers-${_target}
    make DESTDIR=${pkgdir} install
  done

  msg "Installing MinGW-w64 licenses"
  install -Dm644 ${srcdir}/mingw-w64-v${pkgver}/COPYING.MinGW-w64/COPYING.MinGW-w64.txt "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.MinGW-w64.txt"
  install -Dm644 ${srcdir}/mingw-w64-v${pkgver}/COPYING.MinGW-w64-runtime/COPYING.MinGW-w64-runtime.txt "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.MinGW-w64-runtime.txt"
  install -Dm644 ${srcdir}/mingw-w64-v${pkgver}/mingw-w64-headers/ddk/readme.txt "${pkgdir}/usr/share/licenses/${pkgname}/ddk-readme.txt"
  install -Dm644 ${srcdir}/mingw-w64-v${pkgver}/mingw-w64-headers/direct-x/COPYING.LIB "${pkgdir}/usr/share/licenses/${pkgname}/direct-x-COPYING.LIB"
  install -Dm644 ${srcdir}/mingw-w64-v${pkgver}/mingw-w64-headers/direct-x/readme.txt "${pkgdir}/usr/share/licenses/${pkgname}/direct-x-readme.txt"
}

