pkgname=discord
_pkgname=Discord
pkgver=0.0.48
pkgrel=2
pkgdesc="All-in-one voice and text chat for gamers."
arch=('x86_64')
url='https://discord.com/'
license=('custom')
depends=('libnotify' 'libxss' 'nspr' 'nss' 'gtk3')
optdepends=('pulseaudio: PulseAudio is a featureful, general-purpose sound server'
            'pulseaudio-qt: PulseAudio QT library for volume controle in QT environment.'
            'xdg-utils: Open files')
options=('!strip')
install="${pkgname}.install"
source=("${_pkgname}-${pkgver}.tar.gz::https://dl.discordapp.net/apps/linux/${pkgver}/${pkgname}-${pkgver}.tar.gz"
        "Discord--License.pdf"
        "Discord--OSS-License.pdf")
sha512sums=('SKIP' 'SKIP' 'SKIP')

package() {
  mkdir -p "${pkgdir}/opt/"

  bsdtar -xf "${srcdir}/${_pkgname}-${pkgver}.tar.gz" -C "${pkgdir}/opt/"

  msg2 "Removing unnecessary post-installation script from the SOURCE package which included in installation"
  rm -fv "${pkgdir}/opt/${pkgname}/postinst.sh"

  msg2 "Installing application files and thumbnail picture from SOURCE to the system"
  install -v -Dm644 "${pkgdir}/opt/${_pkgname}/${pkgname}.png" -t "${pkgdir}/usr/share/icons/hicolor/256x256/apps/"
  install -v -Dm644 "${pkgdir}/opt/${_pkgname}/${pkgname}.png" -t "${pkgdir}/usr/share/pixmaps/"
  install -v -Dm755 "${pkgdir}/opt/${_pkgname}/${pkgname}.desktop" -t "${pkgdir}/usr/share/applications/"

  sed -i 's|Path=/usr/bin|Path=/opt/Discord/|g' \
  "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  sed -i 's|Exec=/usr/share/discord/Discord|Exec=/usr/bin/discord|g' \
  "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  msg2 "Linking binaries from SOURCE to the system"
  install -d "${pkgdir}/usr/bin/"
  ln -f -v -s "/opt/${_pkgname}/${_pkgname}" "${pkgdir}/usr/bin/${pkgname}"

  msg2 "Impose sandboxing by modifying SUID properties"
  chmod -v 4755 "${pkgdir}/opt/${_pkgname}/chrome-sandbox"
  chmod -v 755 "${pkgdir}/opt/${_pkgname}/${_pkgname}"

  msg2 "Installing Discord proprietary LICENSE from SOURCE into the system"
  install -v -Dm644 "${srcdir}/Discord--License.pdf" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.pdf"
  install -v -Dm644 "${srcdir}/Discord--OSS-License.pdf" "${pkgdir}/usr/share/licenses/${pkgname}/OSS-LICENSE.pdf"
}
