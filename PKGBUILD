pkgname=bibble
pkgver=0.1.0
pkgrel=1
pkgdesc="Bibble SDK"
arch=('x86_64')
url="https://github.com/JannikBulow/Bibble"
license=('Apache-2.0')
makedepends=('cmake' 'git' 'ninja' 'gcc' 'nasm')
depends=()

source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('9bb504c440209446444597414c438caa854a173f9145eb5794d6bb6aa6f7946e') # REMEMBER TO DO updpkgsums WHEN MAKING NEW RELEASE

build() {
    cmake -S "$srcdir/Bibble-$pkgver" \
          -B "$srcdir/Bibble-$pkgver/build" \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DBUILD_TESTING=OFF \
          -DINSTALL_GTEST=OFF

    cmake --build "$srcdir/Bibble-$pkgver/build" --parallel
}

package() {
    DESTDIR="$pkgdir" cmake --install "$srcdir/Bibble-$pkgver/build"
    install -Dm644 "$startdir/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
