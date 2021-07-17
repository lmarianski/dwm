# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
  config.h
  dwm.desktop
  https://dwm.suckless.org/patches/fullgaps/dwm-fullgaps-$pkgver.diff
  https://dwm.suckless.org/patches/xresources/dwm-xresources-$pkgver.diff
  https://dwm.suckless.org/patches/scratchpad/dwm-scratchpad-$pkgver.diff
  https://dwm.suckless.org/patches/transfer/dwm-transfer-$pkgver.diff
  https://dwm.suckless.org/patches/alpha/dwm-alpha-20201019-61bb8b2.diff
  # https://dwm.suckless.org/patches/selfrestart/dwm-r1615-selfrestart.diff
  dwm-r1615-selfrestart.diff
  https://lists.suckless.org/dev/att-7590/shiftview.c
)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'SKIP'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            '3c59104f4b23b8ec3c31ff639712dc1214bd5e3a487f7af039268373eb9e0b2d'
            '24205a155f217676ad6ef5c8f54a0a918556ffe9fe0bc3ba0b157e03a95dfa7c'
            'ffb89eb41d7a5e72471dcf92aed4a1b5dec207e65f23497d0522f15e99ebc29d'
            '25d898b5efa156eb5af12a4ecd114bce64a17f37b92f6498fd2c2f668ca0baff'
            '220d43669ce24e037f8cfe7008893fa05a7da68b00667bc65e558b75a06cd563'
            'e090f711bd37813195efcba98a7e8de49c4b3f2a9f8d90871cd1b79900d80408'
            'a48b1e5a9c4b29d0ebad3dfb3eacf4bacf5188f4d620a921dc852620cf6e6e88')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

  cp "$srcdir/config.h" config.h

  cp "$srcdir/shiftview.c" shiftview.c

  patch --input "$srcdir/dwm-alpha-20201019-61bb8b2.diff"   || echo

  patch --input "$srcdir/dwm-xresources-$pkgver.diff" || echo
  patch --input "$srcdir/dwm-fullgaps-$pkgver.diff"   || echo
  patch --input "$srcdir/dwm-scratchpad-$pkgver.diff" || echo
  patch --input "$srcdir/dwm-transfer-$pkgver.diff"   || echo

  patch --input "$srcdir/dwm-r1615-selfrestart.diff"  || echo

  cp "$srcdir/config.h" config.def.h


  # cp config.def.h.rej "/home/m00n/Dokumenty/dwm/config.def.h.rej"


  # cp "config.def.h" config.h
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
