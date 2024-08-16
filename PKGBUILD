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
source=('git+https://github.com/ginogravanis/st.git')
md5sums=('SKIP')

pkgver() {
   git -C "$srcdir/$pkgname" describe --long --tags | sed 's/-/./g'
}

build() {
   make -C "$srcdir/$pkgname"
}

package() {
   local srcroot="$srcdir/$pkgname"
   local sharedir="$pkgdir/usr/share"
   make -C "$srcroot" PREFIX=/usr DESTDIR="$pkgdir" install
   install -Dm0644 -t "$sharedir/licenses/$pkgname" "$srcroot/LICENSE"
   install -Dm0644 -t "$sharedir/doc/$pkgname" "$srcroot/README.md"
   install -Dm0644 -t "$sharedir/$pkgname" "$srcroot/st.info"
}
