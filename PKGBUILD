# Maintainer: Lea Seibert <mail@lea.moe>
# Contributor: FayBoy <ahmadyasinfikri at gmail dot com>
# Contributor: Ecmel Berk Canlıer <me@ecmelberk.com>
# Contributor: Sven-Hendrik Haase <svenstaro@gmail.com>
# Contributor: philefou <tuxication AT gmail DOT com>
# Contributor: lindquist <tomas@famolsen.dk>
# Contributor: Christoph Siegenthaler <csi@gmx.ch>
# Contributor: Mihai Militaru <mihai.militaru@ephemeros.org>
# Contributor: SpepS <dreamspepser at yahoo dot it>


pkgname=glfw-wayland-minecraft-cursorfix
pkgdesc="A free, open source, portable framework for graphical application development (wayland, patched for Minecraft)"
pkgver=3.5
pkgrel=1
arch=('x86_64')
url="https://github.com/Serverator/glfw-wayland"
license=('custom:ZLIB')
depends=('wayland' 'libxkbcommon' 'libgl')
conflicts=('glfw' 'glfw-wayland' 'glfw-wayland-minecraft-libdecoration')
provides=("glfw=$pkgver")
makedepends=('mesa' 'cmake' 'doxygen' 'vulkan-headers' 'vulkan-icd-loader'
             'extra-cmake-modules' 'wayland-protocols' 'libxi' 'libxrandr'
             'libxcursor' 'libxinerama')
source=("git+https://github.com/Serverator/glfw-wayland")
sha512sums=('SKIP')

prepare() {
  cd "$srcdir/glfw-wayland"
  
  rm -rf ./glfw

  git clone https://github.com/glfw/glfw

  for patch in "$srcdir/glfw-wayland/patches/00"*.patch; do
    echo "Applying patch $patch"
    patch -p1 -d ./glfw < "$patch"
  done
}

build() {
  cd "$srcdir/glfw-wayland/glfw"

  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_INSTALL_LIBDIR=lib \
      -DBUILD_SHARED_LIBS=ON
}

package() {
  cd "$srcdir/glfw-wayland/glfw"

  make DESTDIR=$pkgdir install

  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
