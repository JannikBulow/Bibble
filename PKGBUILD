pkgname=bibble
pkgver=0.1.0
pkgrel=1
pkgdesc="Bibble SDK"
arch=('x86_64')
url="https://github.com/JannikBulow/Bibble"
license=('Apache-2.0')
makedepends=('cmake' 'git')
depends=()

source=("$pkgname-$pkgver.tar.gz::https://github.com/JannikBulow/Bibble/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

build() {
    cmake -S "$srcdir/Bibble-$pkgver" \
          -B "$srcdir/Bibble-$pkgver/build" \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DBUILD_TESTING=OFF \
          -DINSTALL_GTEST=OFF

    cmake --build "$srcdir/Bibble-$pkgver/build" -j
}

package() {
    DESTDIR="$pkgdir" cmake --install "$srcdir/Bibble-$pkgver/build"
}