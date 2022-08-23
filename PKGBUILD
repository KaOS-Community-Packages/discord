pkgname=discord
_pkgname=Discord
pkgver=0.0.19
pkgrel=1
pkgdesc="All-in-one voice and text chat for gamers that's free and secure."
arch=('x86_64')
url='https://discordapp.com'
license=('custom')
depends=('libnotify' 'libxss' 'nspr' 'nss' 'gtk3')
optdepends=('pulseaudio: Pulseaudio support'
            'xdg-utils: Open files')
source=("https://dl.discordapp.net/apps/linux/$pkgver/$pkgname-$pkgver.tar.gz"
        'LICENSE.html::https://discordapp.com/terms'
        'OSS-LICENSES.html::https://discordapp.com/licenses')
sha512sums=('5b73f0f968ce61f5a844940e1525da80e7b2ce3779cf2050ca3c2b0b7dbee20f16e2bf203f0673d1e275d1e55075b83eb63700731be8324587b3c58c64d3a0e8'
            'f29327e2c6653e9c665a5cf351bfec0a3e05ba0b69104139b8753840543fb0180f91f6e187c25f54b8371753be819fd450468160fa8f523fd0c1218997e2f40d'
            'd1acfad7c00de8e9c88ed3a60b0db7fc49f78079548a6b350de33c42ef384b5cacfb14ba243a3c6ec3fece9e82ba6cedd655bc4daa29b149e41fef8536c29a25')

prepare() {
  cd $_pkgname

  sed -i "s|Exec=.*|Exec=/usr/bin/$pkgname|" $pkgname.desktop
  echo 'Path=/usr/bin' >> $pkgname.desktop
}

package() {
  # Install the app
  install -d "$pkgdir"/opt/$pkgname
  cp -a $_pkgname/. "$pkgdir"/opt/$pkgname

  chmod 755 "$pkgdir"/opt/$pkgname/$_pkgname

  rm "$pkgdir"/opt/$pkgname/postinst.sh

  install -d "$pkgdir"/usr/{bin,share/{pixmaps,applications}}
  ln -s /opt/$pkgname/$_pkgname "$pkgdir"/usr/bin/$pkgname
  ln -s /opt/$pkgname/discord.png "$pkgdir"/usr/share/pixmaps/$pkgname.png
  ln -s /opt/$pkgname/$pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop

  # setuid on chrome-sandbox
  chmod u+s "$pkgdir"/opt/$pkgname/chrome-sandbox

  # Licenses
  install -Dm 644 LICENSE.html "$pkgdir"/usr/share/licenses/$pkgname/LICENSE.html
  install -Dm 644 OSS-LICENSES.html "$pkgdir"/usr/share/licenses/$pkgname/OSS-LICENSES.html
}
