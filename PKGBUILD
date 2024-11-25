# Maintainer: Thule <vincenzo.frascino@proton.me>
# Contributor: Neptune <neptune650@proton.me>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.5
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="https://dwm.suckless.org"
arch=('i686' 'x86_64' 'arm' 'armv7h' 'armv6h' 'aarch64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
install=dwm.install
source=(dwm.desktop
        https://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	"https://dwm.suckless.org/patches/keychord/dwm-keychord-6.4.diff"
	"https://dwm.suckless.org/patches/attachaside/dwm-attachaside-6.4.diff"
	"https://dwm.suckless.org/patches/cursorwarp/dwm-cursorwarp-6.3.diff"
	"https://dwm.suckless.org/patches/autostart/dwm-autostart-20210120-cb3f58a.diff"
        config.h)
sha256sums=('bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            '21d79ebfa9f2fb93141836c2666cb81f4784c69d64e7f1b2352f9b970ba09729'
            'daa80d49e37ddd440d2b424a6a7aca9c792d2d96aad869a0800332559f19d6c1'
            'e7dd151e6f54b256bea35ea6d6767f2563d22b48b106c4ff0c65813a38bef3d9'
            '5bacf3ee1e434ace02b4ad7bb47c6cdcb425b7c24cea5867f9ea3119a3323d04'
            'd78711587e6d554de5dc47adca00fc1eb6c8f8ca11c9e75411da8da60eae7abe'
            'a3eabfa1cfe350fe638e5c8e04e72a16ba5618d0372f96ee1e1d7a3974547399')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

  patch -p1 -i "$srcdir/dwm-fibonacci-20200418-c82db69.diff"
  patch -p1 -i "$srcdir/dwm-autostart-20210120-cb3f58a.diff"
  patch -p1 -i "$srcdir/dwm-keychord-6.4.diff"
  patch -p1 -i "$srcdir/dwm-attachaside-6.4.diff"
  patch -p1 -i  "$srcdir/dwm-cursorwarp-6.3.diff"
  if [[ -f "$srcdir/config.h" ]]; then
    cp -fv "$srcdir/config.h" config.h
  fi
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  install -Dm644 "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
