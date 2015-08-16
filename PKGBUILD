# Maintainer: Cedric Girard <girard.cedric@gmail.com>
# Contributor: Lukas Fleischer <archlinux at cryptocrack dot de>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Andreas Wagner <a.wagner@stud.uni-frankfurt.de>

pkgname=lockdev-fpic
_pkgname=lockdev
provides=('lockdev')
conflicts=('lockdev')
pkgver=1.0.3_1.5
_pkgver=1.0.3
pkgrel=1
pkgdesc='Run-time shared library for locking devices, using _both_ FSSTND and SVr4 methods.'
url='http://packages.qa.debian.org/l/lockdev.html'
license=("GPL")
arch=('i686' 'x86_64')
source=("http://ftp.debian.org/debian/pool/main/l/${_pkgname}/${_pkgname}_${_pkgver}.orig.tar.gz"
	      "http://ftp.debian.org/debian/pool/main/l/${_pkgname}/${_pkgname}_${pkgver/_/-}.diff.gz")
md5sums=('64b9c1b87b125fc348e892e24625524a'
         'c4e8a5a2e46b76b48339c232b358f579')

build() {
  cd "${_pkgname}-${_pkgver}"

  patch -p1 -i "../${_pkgname}_${pkgver/_/-}.diff"
  sed -i "s|CFLAGS	= -g|CFLAGS	= -g -fPIC|" Makefile

  make shared CFLAGS="${CFLAGS} -fPIC -D_PATH_LOCK=\\\"/run/lock/lockdev\\\""
  make static CFLAGS="${CFLAGS} -fPIC -D_PATH_LOCK=\\\"/run/lock/lockdev\\\""
}

package() {
  cd "${_pkgname}-${_pkgver}"
  make basedir="${pkgdir}/usr" install
}
