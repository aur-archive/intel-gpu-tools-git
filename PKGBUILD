# Maintainer: bslackr <brendan at vastactive dot com>
# Contributor: Alexander Lam <lambchop468 *at* gmail *dot* com>

pkgname=intel-gpu-tools-git
pkgver=20130224
pkgrel=2
pkgdesc="Tools for development and testing of the Intel DRM driver"
url="http://lists.freedesktop.org/archives/xorg/2009-April/045350.html"
arch=('i686' 'x86_64')
license=('custom')
depends=('libdrm' 'libpciaccess')
makedepends=('git' 'xorg-util-macros' 'swig')
conflicts=('intel-gpu-tools')

_gitroot="git://anongit.freedesktop.org/git/xorg/app/intel-gpu-tools"
_gitname="intel-gpu-tools"

build() {
  msg "Connecting to git.freedesktop.org GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
    cd $_gitname
  fi
  
  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  ./autogen.sh --prefix=/usr PYTHON_LDFLAGS="-lpython3.3m"
  make
}

package() {
  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -m 644 "$srcdir/$_gitname/COPYING" "$pkgdir/usr/share/licenses/$pkgname"
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir" install
}
