#!/usr/bin/env bash
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
   'https://st.suckless.org/patches/scrollback/st-scrollback-0.8.5.diff'
   'https://st.suckless.org/patches/scrollback/st-scrollback-reflow-0.8.5.diff'
   'https://st.suckless.org/patches/scrollback/st-scrollback-mouse-20220127-2c5edf2.diff'
   'https://st.suckless.org/patches/scrollback/st-scrollback-mouse-altscreen-20220127-2c5edf2.diff'
)
extra_patches=(
   'font-size.diff'
   'scroll-increment.diff'
   'boxdraw.diff'
   'simple_plumb-0.8.5.diff'
)
md5sums=(
   'SKIP'
   '11d65e7ad4905c984f6a4a4c83857031'
   '76560e904326f9dda8693b72686c7ac5'
   '2540178ff4c1ead78a7249d1d9939d52'
   'dbe85797bd1fd8099b032e6f7cc2112c'
   '988cbd4c8612dbe1b6f1845d06cfc6f0'
   'd740e376ed70ed719f5d68e44755e861'
)

prepare() {
   local srcroot="$srcdir/$pkgname"
   git -C "$srcroot" clean -f
   for patch in "${source[@]:1}" "${extra_patches[@]}"; do
      echo "[patch] Applying $(basename "$patch")..."
      patch -d "$srcroot" -p1 -i "$BUILDDIR/$(basename "$patch")"
      echo "[patch] ... done"
   done
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
   make -C "$srcdir/$pkgname" PREFIX=/usr DESTDIR="$pkgdir/" install
   install -Dm644 "$srcroot/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
   install -Dm644 "$srcroot/README" "$pkgdir/usr/share/doc/$pkgname/README"
}
