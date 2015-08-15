# Maintainer: Qhor Vertoe <vertoe at qhor dot net>

# Contributor: Noel Maersk <veox at wemakethings dot net>
# Contributor: Mike Lenzen <lenzenmi at gmail dot com>

pkgname=bitshares-x
_gitname=bitsharesx
pkgver=0.4.20
pkgrel=1
pkgdesc="BitShares X is a peer-to-peer network-based digital asset exchange."
arch=('i686' 'x86_64')
url="http://bitshares-x.info/"
license=('MIT')
depends=('qt5-base>=5.3' 'boost-libs>=1.52' 'miniupnpc>=1.6')
makedepends=('git' 'boost' 'clang' 'make' 'nodejs')
provides=('bitshares-x')
source=('git://github.com/dacsunlimited/bitsharesx.git')
md5sums=('SKIP')

build() {
  cd "$srcdir/$_gitname"

  # Prepare dependencies
  git submodule init
  git submodule update

  # Checkout release
  git checkout v$pkgver

  cd $srcdir/$_gitname/programs/web_wallet
  sudo npm install -g lineman
  npm install

  # Configure and compile the wallet
  cd "$srcdir/$_gitname"
  CC=clang CXX=clang++ cmake -DINCLUDE_QT_WALLET=ON .
  CC=clang CXX=clang++ make $MAKEFLAGS -j $(nproc) buildweb
  CC=clang CXX=clang++ make $MAKEFLAGS -j $(nproc)
}

package() {
  # Install BitShares-X Qt-wallet
  install -D -m755 "$srcdir/$_gitname/programs/qt_wallet/bin/BitSharesX" "$pkgdir/usr/bin/BitShares-X"

  # Install license
  install -D -m644 "$srcdir/$_gitname/LICENSE.md" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}

