# Maintainer: Gino Gravanis

pkgname=st
pkgver=1
pkgrel=1
pkgdesc='Simple terminal for X'
arch=('i686' 'x86_64')
url='https://st.suckless.org/'
license=('MIT')
depends=()
makedepends=('git')
provides=()
conflicts=()
source=(
   'git+https://git.suckless.org/st'
   'https://st.suckless.org/patches/gruvbox/st-gruvbox-dark-0.8.5.diff'
   'https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff'
)
md5sums=(
   'SKIP'
   '11d65e7ad4905c984f6a4a4c83857031'
   '76560e904326f9dda8693b72686c7ac5'
)

prepare() {
   local srcroot="$srcdir/$pkgname"
   for patch in "${source[@]:1}"; do
      patch -d "$srcroot" -p1 -i "$BUILDDIR/$(basename $patch)"
   done
   patch -d "$srcroot" -p1 -i "$BUILDDIR/font-size.diff"
   cp "$srcroot/config.def.h" "$srcroot/config.h"
}

pkgver() {
   git -C "$srcdir/$pkgname" describe --long --tags | sed 's/-/./g'
}

build() {
   make -C "$srcdir/$pkgname"
}

package() {
   local srcroot="$srcdir/$pkgname"
   local license_dir="$pkgdir/usr/share/licenses/$pkgname"
   make -C "$srcdir/$pkgname" PREFIX=/usr DESTDIR="$pkgdir/" install
   install -Dm644 "$srcroot/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
   install -Dm644 "$srcroot/README" "$pkgdir/usr/share/doc/$pkgname/README"
}
