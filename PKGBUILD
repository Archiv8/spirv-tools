#!/bin/bash

# Based on original packaging by Laurent Carlier <lordheavym@gmail.com>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/spirv-tools/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/spirv-tools/discussions>

_relname="SPIRV-Tools"

pkgname=spirv-tools
pkgver=1.3.216.0
pkgrel=1
pkgdesc="API and commands for processing SPIR-V modules"
arch=(
  "x86_64"
)
url="https://www.khronos.org/vulkan/"
license=(
  "custom"
)
groups=(
  "vulkan-devel"
)
depends=(
  # Official Arch Linux
  "gcc-libs"
)
makedepends=(
  # Official Arch Linux
  "cmake"
  "python"
  "git"
  "ninja"

  # Archiv8 / AUR
  "spirv-headers"
)
# https://github.com/KhronosGroup/SPIRV-Tools/archive/refs/tags/v2022.2.tar.gz
_tarname="${_relname}-sdk-${pkgver}"
source=(
  "${_tarname}.tar.gz"::"https://github.com/KhronosGroup/${_relname}/archive/refs/tags/sdk-${pkgver}.tar.gz"
)
sha512sums=(
  "2d7f18e00a13a26f7aec81a2e5aca39a8f2e2801018aedd2d4332096e9dcea9e336527438acce381608cb6612eca034c6147795c207016403ee7201ed0c327eb"
)

build() {
  cd "${srcdir}/${_tarname}"

  cmake \
    -Bbuild \
    -GNinja \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_BUILD_TYPE=Release \
    -DSPIRV_WERROR=Off \
    -DBUILD_SHARED_LIBS=ON \
    -DSPIRV_TOOLS_BUILD_STATIC=OFF \
    -DSPIRV-Headers_SOURCE_DIR=/usr

  ninja -C build
}

package() {

  cd "${srcdir}/${_tarname}"

  DESTDIR="${pkgdir}" ninja -C build install

  install -Dm644 LICENSE "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}
