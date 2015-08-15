# Maintainer: kuri <sysegv@gmail.com>
# Contributor: chefpeyo <pierre-olivier.huguet@asp64.com>

pkgname=esskyuehl-svn
pkgver=83598
pkgrel=1
pkgdesc="Esskyuehl (ESQL) is a completely asynchronous client-side SQL library."
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL2.1')
depends=('eina' 'ecore')
makedepends=('subversion')
optdepends=('libmysqlclient' 'sqlite' 'postgresql-libs')
options=('!libtool')
source=()
md5sums=()

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/PROTO/esskyuehl"
_svnmod="esskyuehl"

build() {
  cd $srcdir

  if [ $NOEXTRACT -eq 0 ]; then
    msg "Connecting to $_svntrunk SVN server...."
    if [ -d $_svnmod/.svn ]; then
      (cd $_svnmod && svn up -r $pkgver)
    else
      svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
    fi

    msg "SVN checkout done or server timeout"
    msg "Starting make..."

  fi
  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build

  ./autogen.sh --prefix=/usr 
  make || return 1
  make DESTDIR=$pkgdir install || return 1

# install license files
  install -Dm644 $srcdir/$_svnmod-build/COPYING \
  	$pkgdir/usr/share/licenses/$pkgname/COPYING

  rm -r $startdir/src/$_svnmod-build
}
