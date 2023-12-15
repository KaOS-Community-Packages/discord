pkgname=discord
_pkgname=Discord
pkgver=0.0.38
pkgrel=1
pkgdesc="All-in-one voice and text chat for gamers."
arch=('x86_64')
url='https://discord.com/'
license=('custom')
depends=('libnotify' 'libxss' 'nspr' 'nss' 'gtk3')
optdepends=('pulseaudio: PulseAudio is a featureful, general-purpose sound server'
            'pulseaudio-qt: PulseAudio QT library for volume controle in QT environment.'
            'xdg-utils: Open files')
source=("${pkgname}-${pkgver}.tar.gz::https://dl.discordapp.net/apps/linux/${pkgver}/${pkgname}-${pkgver}.tar.gz"
        "LICENSE-${pkgver}.html::https://discordapp.com/terms"
        "OSS-LICENSES-${pkgver}.html::https://discordapp.com/licenses")
sha512sums=('SKIP' 'SKIP' 'SKIP')
options=(!strip)

prepare() {
  cd "${_pkgname}/"
  sed -i "s|Exec=.*|Exec=/usr/bin/${pkgname}|" "${pkgname}.desktop"
}

package() {
  install -d "${pkgdir}"/opt/${pkgname}/
  cp -a "${_pkgname}/." "${pkgdir}"/opt/${pkgname}/

  chmod 755 "${pkgdir}/opt/${pkgname}/${_pkgname}"

  rm -f "${pkgdir}/opt/${pkgname}/postinst.sh"

  install -d "${pkgdir}/usr/bin/"
  ln -s "/opt/${pkgname}/${_pkgname}" -t "${pkgdir}/usr/bin/"

  install -d "${pkgdir}/usr/share/applications"
  ln -s /opt/${pkgname}/${pkgname}.desktop -t "${pkgdir}/usr/share/applications/"

  install -d "${pkgdir}/usr/share/icons/hicolor/256x256/apps"
  ln -s "/opt/${pkgname}/${pkgname}.png" -t "${pkgdir}/usr/share/icons/hicolor/256x256/apps/"

  # setuid on chrome-sandbox
  chmod u+s "${pkgdir}/opt/${pkgname}/chrome-sandbox"

  install -Dm644 "./LICENSE-${pkgver}.html" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.html"
  install -Dm644 "OSS-LICENSES-${pkgver}.html" "${pkgdir}/usr/share/licenses/${pkgname}/OSS-LICENSES.html"
}
