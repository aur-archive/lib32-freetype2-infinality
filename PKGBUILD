# Maintainer: Shanto <shanto@hotmail.com>
# Contributor: JIN Xiao-Yong <jinxiaoyong@gmail.com>
# Contributor: Andre Fettouhi <A.Fettouhi@gmail.com>

_pkgbasename=freetype2-infinality
pkgname=lib32-$_pkgbasename
pkgver=2.4.12
pkgrel=2
_pkgdate=20130514
_pkgrel=01
pkgdesc="TrueType font rendering library (32-bit) with infinality patch"
arch=(x86_64)
license=('GPL')
url="http://www.infinality.net/blog/infinality-freetype-patches/"
depends=('lib32-zlib' 'lib32-bzip2' $_pkgbasename)
makedepends=(gcc-multilib)
conflicts=('lib32-freetype2')
provides=("lib32-freetype2=$pkgver")
options=('!libtool')
source=(
	"http://downloads.sourceforge.net/sourceforge/freetype/freetype-${pkgver}.tar.bz2"
	"http://www.infinality.net/fedora/linux/zips/freetype-infinality-${pkgver}-${_pkgdate}_${_pkgrel}-x86_64.tar.bz2"
	"freetype-2.2.1-enable-valid.patch::https://projects.archlinux.org/svntogit/packages.git/plain/trunk/freetype-2.2.1-enable-valid.patch?h=packages/freetype2"
)
build() {
	export CC="gcc -m32"
	export CXX="g++ -m32"
	export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"
	rm -rf "${srcdir}/freetype-${pkgver}-build"
	cp -a "${srcdir}/freetype-${pkgver}" "${srcdir}/freetype-${pkgver}-build"
	cd "${srcdir}/freetype-${pkgver}-build"
	cat "$srcdir/"{freetype-2.2.1-enable-valid.patch,freetype-entire-infinality-patchset-20130514-01.patch} | patch -Np1
	./configure --prefix=/usr --libdir=/usr/lib32
	make
}
package() {
	cd "${srcdir}/freetype-${pkgver}-build"
	make DESTDIR="${pkgdir}" install
	rm -rf "${pkgdir}"/usr/{include,share,bin}
}
md5sums=('3463102764315eb86c0d3c2e1f3ffb7d'
         '4f5ff3fd3e3e56310953e25eade4a2d3'
         '214119610444c9b02766ccee5e220680')
