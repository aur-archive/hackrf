# Maintainer: Dominik Heidler <dheidler@gmail.com>
pkgname=hackrf
pkgver=2013.07.1
pkgrel=2
pkgdesc="Driver for HackRF, allowing general purpose software defined radio (SDR)."
arch=('i686' 'x86_64')
url="https://github.com/mossmann/hackrf"
license=('GPLv2')
depends=('libusb')
makedepends=('cmake')

source=("http://downloads.sourceforge.net/${pkgname}/${pkgname}-${pkgver}.tar.xz" "52-hackrf.rules")
md5sums=('f66ec1273f573e0728366c3ecd3e52f3'
         '8fed871905d2765e1c4fb0e656dd4900')

build() {
	cd "$srcdir/${pkgname}-${pkgver}/host"
	mkdir -p build
	cd build
	cmake \
		-DCMAKE_INSTALL_PREFIX=/usr ../
	make
}

package() {
	cd "$srcdir/${pkgname}-${pkgver}/host/build"
	make DESTDIR=${pkgdir} install
	cd "$srcdir"
	install -vD -m644 52-hackrf.rules $pkgdir/usr/lib/udev/rules.d/52-hackrf.rules
	cd "$srcdir/${pkgname}-${pkgver}/firmware-bin"
	install -vD -m644 hackrf_usb_rom_to_ram.bin $pkgdir/usr/share/hackrf/hackrf_usb_rom_to_ram.bin
}
