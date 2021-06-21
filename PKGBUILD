# Maintainer: Gabriel Carneiro <therealcarneiro at gmail dot com>

pkgname=astraltabletop-nativefier
_pkgname=AstralTableTop
pkgver=1.0
pkgrel=1
pkgdesc="Astral TableTop desktop built with nativefier (electron)"
arch=("armv7l" "i686" "x86_64")
url="https://app.${pkgname%-nativefier}.com"
license=("custom")
depends=("gtk3" "libxss" "nss")
optdepends=("libindicator-gtk3")
makedepends=("imagemagick" "nodejs-nativefier" "unzip")
source=(
  "${pkgname}.desktop"
  "${pkgname}.png"
)
md5sums=(
  'SKIP'
  'SKIP'
)

build() {
  cd "${srcdir}"
  
  nativefier \
    --name "${_pkgname}" \
    --icon "${pkgname}.png" \
    --verbose \
    --single-instance \
    "${url}"
}

package() {
  install -dm755 "${pkgdir}/"{opt,usr/{bin,share/{applications,licenses/${pkgname}}}}

  _folder="${_pkgname}-linux-x64"
  _binary="/opt/${pkgname}/${_pkgname}"

  cp -rL "${srcdir}/${_folder}" "${pkgdir}/opt/${pkgname}"
  ln -s "${_binary}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm644 "${pkgdir}/opt/${pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  for _size in "192x192" "128x128" "96x96" "64x64" "48x48" "32x32" "24x24" "22x22" "20x20" "16x16" "8x8"
  do
    install -dm755 "${pkgdir}/usr/share/icons/hicolor/${_size}/apps"
    convert "${srcdir}/${pkgname}.png" -strip -resize "${_size}" "${pkgdir}/usr/share/icons/hicolor/${_size}/apps/${pkgname}.png"
  done
}
