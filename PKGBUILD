# Maintainer: csmantle <aur at csmantle dot top>
# shellcheck shell=bash
# shellcheck disable=SC2034,SC2154,SC2164

_pkgname=libldrm
pkgname="${_pkgname}-bin"
_origver='1.0.2-lnd25.1~rc1.7'
_pkgver="$(printf '%s' "$_origver" | tr -- '-~' '_.')"
pkgver="$_pkgver"
pkgrel=2
pkgdesc='DRM (Direct Rendering Manager) interface library for LoongGPU'
arch=('loong64')
url='https://pkg.loongnix.cn/'
license=('LicenseRef-Proprietary')
depends=('glibc')
provides=("$_pkgname")
conflicts=("$_pkgname")
options=('!debug' '!strip')

_debname="${_pkgname}_${_origver}_loong64.deb"
source=("${_debname}::https://pkg.loongnix.cn/loongnix/25/pool/non-free/l/loonggpu-graphics-drivers/${_debname}")
sha256sums=('68d1639d38d5c01b5a646562126a0e0dba5f8182719280573d3fc1f7c7e06e6a')

package() {
  echo 'Unpacking ldrm ...'
  bsdtar -xvf "$_debname"
  tar -xvf data.tar.* -C "$pkgdir"

  echo 'Moving libraries to the correct location ...'
  mkdir -p "$pkgdir"/usr/lib
  mv -v "$pkgdir"/usr/lib/loongarch64-linux-gnu/* "$pkgdir"/usr/lib/
  rm -vrf "$pkgdir"/usr/lib/loongarch64-linux-gnu

  echo 'Setting executable bits for shared objects ...'
  chmod -v +x "$pkgdir"/usr/lib/*.so*

  echo 'Installing license ...'
  install -vDm644 "$pkgdir"/usr/share/doc/"$_pkgname"/copyright "$pkgdir"/usr/share/licenses/"$pkgname"/LICENSE
}

