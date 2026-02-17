_realname=jank
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
pkgver=0.0.1
pkgrel="local"
pkgdesc="The native Clojure dialect hosted on LLVM with seamless C++ interop. (mingw-w64)"
arch=('any')
mingw_arch=('clang64')
url="https://github.com/ikappaki/jank-win"
msys2_references=(
  "cpe: cpe:/a:jank:jank"
)
license=('spdx:MPL-2.0')
depends=("${MINGW_PACKAGE_PREFIX}-openssl"
         "${MINGW_PACKAGE_PREFIX}-winpthreads"
         "${MINGW_PACKAGE_PREFIX}-zlib"
         "${MINGW_PACKAGE_PREFIX}-zstd"
        )
makedepends=("git"
             "${MINGW_PACKAGE_PREFIX}-clang"
             "${MINGW_PACKAGE_PREFIX}-cmake"
             "${MINGW_PACKAGE_PREFIX}-dlfcn"
             "${MINGW_PACKAGE_PREFIX}-ninja"
            )
# source=("jank-win")
# noextract=("jank-win")
# sha256sums=('SKIP')

# prepare() {
#     cd "${srcdir}/jank-win"
#     git submodule update --init --recursive --depth 1
# }

build() {
  cd "${srcdir}/jank-win/compiler+runtime"

  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  ./bin/configure \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -GNinja \
    -DCMAKE_BUILD_TYPE=Release

  ./bin/compile
}

package() {
  cd "${srcdir}/jank-win/compiler+runtime"
  DESTDIR="${pkgdir}" ${MINGW_PREFIX}/bin/cmake --install ./build
}
