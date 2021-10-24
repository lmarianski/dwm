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
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	dwm.desktop
	# https://dwm.suckless.org/patches/selfrestart/dwm-r1615-selfrestart.diff
	dwm-r1615-selfrestart.diff
	https://lists.suckless.org/dev/att-7590/shiftview.c
	https://dwm.suckless.org/patches/fullgaps/dwm-fullgaps-$pkgver.diff
	https://dwm.suckless.org/patches/xresources/dwm-xresources-$pkgver.diff
	https://dwm.suckless.org/patches/scratchpad/dwm-scratchpad-$pkgver.diff
	https://dwm.suckless.org/patches/transfer/dwm-transfer-$pkgver.diff
	https://dwm.suckless.org/patches/alpha/dwm-alpha-20201019-61bb8b2.diff
	https://dwm.suckless.org/patches/moveresize/dwm-moveresize-20201206-cce77d8.diff
	https://github.com/mihirlad55/dwm-ipc/releases/download/v1.5.7/dwm-ipc-20201106-f04cac6.diff
	https://dwm.suckless.org/patches/anybar/dwm-anybar-polybar-tray-fix-20200810-bb2e722.diff
	# https://dwm.suckless.org/patches/mpdcontrol/dwm-r1615-mpdcontrol.diff
	# dwm-mpdcontrol-alpha-fix.diff
)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            'e090f711bd37813195efcba98a7e8de49c4b3f2a9f8d90871cd1b79900d80408'
            'a48b1e5a9c4b29d0ebad3dfb3eacf4bacf5188f4d620a921dc852620cf6e6e88'
            '3c59104f4b23b8ec3c31ff639712dc1214bd5e3a487f7af039268373eb9e0b2d'
            '24205a155f217676ad6ef5c8f54a0a918556ffe9fe0bc3ba0b157e03a95dfa7c'
            'ffb89eb41d7a5e72471dcf92aed4a1b5dec207e65f23497d0522f15e99ebc29d'
            '25d898b5efa156eb5af12a4ecd114bce64a17f37b92f6498fd2c2f668ca0baff'
            '220d43669ce24e037f8cfe7008893fa05a7da68b00667bc65e558b75a06cd563'
            '0c8c2305bbb64475f89d332340e6a6e78b32c9e847b7b0aa36d4dda9dad9034d'
            '497f2ebf639c3eeba28ce21f73b7efd2ef2fc045466e43523231094472112da1'
            '60d0bf1a071b83f9c64b5a401ecfa3ea79e84fcf73d19a332816e136b4b43960')

prepare() {
	cd "$srcdir/$pkgname-$pkgver"

	# cp "$srcdir/config.h" config.h

	cp "$srcdir/shiftview.c" shiftview.c
	patch --input "$srcdir/dwm-alpha-20201019-61bb8b2.diff"   || echo

	# patch --input "$srcdir/dwm-ipc-20201106-f04cac6.diff"  || echo

	patch --input "$srcdir/dwm-xresources-$pkgver.diff" || echo
	patch --input "$srcdir/dwm-fullgaps-$pkgver.diff"   || echo
	patch --input "$srcdir/dwm-scratchpad-$pkgver.diff" || echo
	patch --input "$srcdir/dwm-transfer-$pkgver.diff"   || echo
	patch --input "$srcdir/dwm-moveresize-20201206-cce77d8.diff"   || echo
	patch --input "$srcdir/dwm-r1615-selfrestart.diff"  || echo
	# patch --input "$srcdir/dwm-r1615-mpdcontrol.diff"   || echo
	# patch --input "$srcdir/dwm-mpdcontrol-alpha-fix.diff"  || echo

	# patch --input "$srcdir/dwm-anybar-polybar-tray-fix-20200810-bb2e722.diff"  || echo

	# cp "$srcdir/config.h" config.def.h
	# cp config.def.h.rej "/home/m00n/Dokumenty/dwm/config.def.h.rej"
	# cp "config.def.h" config.h

	# This package provides a mechanism to provide a custom config.h. Multiple
	# configuration states are determined by the presence of two files in
	# $BUILDDIR:
	#
	# config.h  config.def.h  state
	# ========  ============  =====
	# absent    absent        Initial state. The user receives a message on how
	#                         to configure this package.
	# absent    present       The user was previously made aware of the
	#                         configuration options and has not made any
	#                         configuration changes. The package is built using
	#                         default values.
	# present                 The user has supplied his or her configuration. The
	#                         file will be copied to $srcdir and used during
	#                         build.
	#
	# After this test, config.def.h is copied from $srcdir to $BUILDDIR to
	# provide an up to date template for the user.
	echo $srcdir

	if [ -e "$BUILDDIR/config.h" ]
	then
		cp "$BUILDDIR/config.h" .
	elif [ ! -e "$BUILDDIR/config.def.h" ]
	then
		msg='This package can be configured in config.h. Copy the config.def.h '
		msg+='that was just placed into the package directory to config.h and '
		msg+='modify it to change the configuration. Or just leave it alone to '
		msg+='continue to use default values.'
		echo "$msg"
	fi
	cp config.def.h "$BUILDDIR"
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
