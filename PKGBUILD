# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Alexandre Bury <alexandre.bury@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=maturin
pkgname="${_py}-${_pkg}"
pkgver=0.14.13
pkgrel=2
_pkgdesc=(
  "Build and publish crates with pyo3,"
  "rust-cpython, cffi and uniffi bindings"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  "x86_64"
  'arm'
  'aarch64'
  'armv7l'
  'pentium4'
  'i686'
  'powerpc'
  'mips'
)
url="https://www.maturin.rs/"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-tomli"
  'maturin'
)
optdepends=(
  "${_py}-pypatchelf"
  )  # TODO: include python-zig when/if it's available in AUR
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-setuptools"
  "${_py}-tomli"
  "${_py}-setuptools-rust"
)
_pypa="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
b2sums=(
  "4218f272ce76b8b2d17db82282552b82ab51d45165bbafb4f2c9b54c872af9716b19d6ebc7dc87a65f615061fcb23d002b855391a3e8aa6142ead58934e766b9"
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m build \
    --wheel \
    --no-isolation
}


package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  mkdir \
    -p \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  cp \
    license-apache \
    license-mit \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
  # The `maturin` binary is provided
  # separately by the maturin package.
  rm \
    "${pkgdir}/usr/bin/maturin"
}
