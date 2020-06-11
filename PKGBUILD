# Maintainer: Brad Fanella <cesura@archlinux.org
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=libmateweather
pkgver=1.24.0
pkgrel=1
pkgdesc="Provides access to weather information from the Internet."
url="https://mate-desktop.org"
arch=('x86_64')
license=('LGPL')
depends=('gtk3' 'libsoup' 'gettext')
conflicts=('libmateweather-gtk3')
replaces=('libmateweather-gtk3')
source=("https://pub.mate-desktop.org/releases/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"
        weather.patch)
sha256sums=('0d6d18296a7011459c92785052ee9a8d695e7fd0bf9d8fa4cc2ce1fe19b59524'
            'SKIP')

build() {
    	cd "${pkgname}-${pkgver}"
    	patch -p1 -i ../weather.patch
    	./configure \
        	--prefix=/usr \
        	--sysconfdir=/etc \
        	--localstatedir=/var \
        	--disable-python \
        	--enable-locations-compression

    	#https://bugzilla.gnome.org/show_bug.cgi?id=656231
    	sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

    	make
}

package() {
    	cd "${pkgname}-${pkgver}"
    	make DESTDIR="${pkgdir}" install
}
