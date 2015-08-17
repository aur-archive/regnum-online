# Maintainer: Vasco Nunes <vascomfnunes at gmail.com>
# Original Submiter: Frikilinux <frikilinux at frikilinux.com.ar>

pkgname=regnum-online
pkgver=1.9.6
pkgrel=1
pkgdesc="Cross-platform 3D Massively Multiplayer Online Role-playing Game (MMORPG)"
arch=('i686' 'x86_64')
_arch=32
url="http://www.regnumonline.com.ar"
license=('custom:Regnum Online License Agreement')
depends=('gtk2' 'mesa' 'openal' 'libjpeg' 'libpng12' 'libvorbis' 'libtheora')
makedepends=()
install=regnum-online.install
options=(!strip)
         
md5sums=('cb0c86923885f5e2971af845672b63e7'
         '37626bbc11916c444bdc20c63efe1d6e'
         '51ac27deb5390ab360bbc8820f440325'
         'c12f01458189445a2db477601f395f22'
         '84ab2767f1815869d8b05ce1959dc1d6')

[ "$CARCH" = "x86_64" ] && md5sums[0]='2c29a8863003fc5f7f71277e9c47955f'
[ "$CARCH" = "x86_64" ] && _arch=64
[ "$CARCH" = "x86_64" ] && makedepends=('lib32-glibc')

# For gzip compression
PKGEXT='.pkg.tar.gz'

source=(http://download01.regnumonlinegame.com/downloads/installer/ROInstall_$_arch
	regnum-online.desktop
	regnum-online
	LICENSE
	regnum.png)

build() {
        cd "${srcdir}"
        mkdir -p reg-extract
        chmod +x ROInstall_$_arch
        ./ROInstall_$_arch --temp ${srcdir} --prefix "${srcdir}"/reg-extract --mode silent
}
package() {
        mkdir -p "${pkgdir}"/opt/regnum
        cd "${pkgdir}"/opt/regnum
        mv -f "${srcdir}"/reg-extract/* .
        rm -rf */
        rm -rf {uninstall,RegnumOnline.exe}
        find -type f -exec chmod 664 {} +
        chmod +x rolauncher
        chmod 775 "${pkgdir}"/opt/regnum
        chown -R root:games "${pkgdir}"/opt/regnum
        install -Dm755 "${srcdir}"/regnum-online "${pkgdir}"/usr/bin/$pkgname
        install -Dm644 "${srcdir}"/LICENSE "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
        install -Dm644 "${srcdir}"/regnum-online.desktop "${pkgdir}"/usr/share/applications/${pkgname}.desktop
        install -Dm644 "${srcdir}"/regnum.png "${pkgdir}"/usr/share/pixmaps/regnum.png
}
