# Maintainer: bjoern lindig <bjoern dot lindig at gmail dot com>
pkgname=pd-net-svn
pkgver=17265
pkgrel=2
pkgdesc="Net objects for pure data (pd) that work with OSC objects among other things..."
arch=('x86_64' 'i686')
url="http://puredata.info/Members/martinrp/"
license=('GPL')
groups=()
depends=('pd' 'glibc')
makedepends=('subversion')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
source=()
noextract=()
#md5sums=() #generate with 'makepkg -g'

_svntrunk=svn://svn.code.sf.net/p/pure-data/svn/trunk/externals/mrpeach/net
_svnmod=net

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  sed -i 's|usr/local|usr|g' Makefile
  sed -i 's|pd-externals|pd/extra|g' Makefile

  #
  # BUILD HERE
  #
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
