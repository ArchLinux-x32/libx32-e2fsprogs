# $Id: PKGBUILD 142655 2015-10-01 16:33:42Z foutrelis $
# Maintainer:  Ionut Biru <ibiru@archlinux.org>
# Contributor: mightyjaym <jm.ambrosino@free.fr>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>

_pkgbasename=e2fsprogs
pkgname=lib32-e2fsprogs
pkgver=1.42.13
pkgrel=1
pkgdesc="Ext2 filesystem libraries (32-bit)"
arch=('x86_64')
license=('GPL' 'LGPL' 'MIT')
url="http://e2fsprogs.sourceforge.net"
depends=('lib32-util-linux' $_pkgbasename)
makedepends=('bc' 'gcc-multilib')
source=("http://downloads.sourceforge.net/sourceforge/${_pkgbasename}/${_pkgbasename}-${pkgver}.tar.gz")
sha1sums=('77d1412472ac5a67f8954166ec16c37616074c37')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  ./configure --prefix=/usr --libdir=/usr/lib32 --with-root-prefix="" --enable-elf-shlibs \
      --disable-{debugfs,imager,resizer,fsck,uuidd,libuuid,libblkid}
  make
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make DESTDIR="${pkgdir}" install-libs

  rm -rf "${pkgdir}"/usr/{bin,include,share}
  mkdir -p "$pkgdir/usr/share/licenses"
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname"
}
