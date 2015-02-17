# Maintainer: zxalexis (zxalexis@gmail.com)
# Contributor: Denis Pershev (napaster@opentech.ru)
# Contributor: Konstantin Shalygin (k0ste@opentech.ru)

pkgname='sac-linux'
pkgver='8.3.34'
pkgrel='2'
pkgdesc='Safenet Authentication Client for Alladin eToken'
arch=('i686' 'x86_64')
url='http://www.aladdin-rd.ru/'
depends=('hal-flash' 'pcsclite' 'pcsc-tools' 'libmtp' 'libusb-compat' 'opensc' 'libpng12' 'gtk2' 'libsm' 'pcsclite')
makedepends=('libarchive')
license='custom'
install='sac.install'
source=('http://online.payment.ru/drivers/SAC_8.3_Linux_10.12.2013.zip' 'sac.install' 'etoken.service')
sha256sums=('d06a2d6071cfd5a8eb1410998a95bb9a8e082b117e04bfe5a38c56879118b7cc' '2f114268e07949d4b15c0e2069e7844d464380e46e892cb13a67341895ca85bd' 'f33a109f85ae71b6b7c2a62ab861831913f9c3e1b4a0223ada28f2deba831c1e')
path='Installation/Standard/DEB'

if [[ "$CARCH" == 'i686' ]]; then
    myarch="i386"
fi

if [[ "$CARCH" == 'x86_64' ]]; then
    myarch="amd64"
fi

build() {
cd "$srcdir/${path}"
bsdtar xf "$srcdir/${path}/SafenetAuthenticationClient-"$pkgver"-0_"${myarch}".deb" && bsdtar xf "$srcdir/${path}/data.tar.gz"
mkdir -p "$srcdir/usr/lib/pcsc/drivers"
mkdir -p "$srcdir/usr/share/eToken"
cp -dpr --no-preserve=ownership "$srcdir/${path}/usr/bin" "$srcdir/usr"
cp -dpr --no-preserve=ownership "$srcdir/${path}/usr/share/eToken/drivers" "$srcdir/usr/share/eToken"
cp -dpr --no-preserve=ownership "$srcdir/${path}/usr/share/eToken/languages" "$srcdir/usr/share/eToken"
cp -dpr --no-preserve=ownership "$srcdir/${path}/lib" "$srcdir/usr"
}

package() {
mkdir -p "$pkgdir/usr/lib/pcsc/drivers"
mkdir -p "$pkgdir/var/cache/eToken"
cp -dpr --no-preserve=ownership "$srcdir/usr" "$pkgdir"
install -Dm 644 "$srcdir/${path}/etc/eToken.conf" "$pkgdir/etc/eToken.conf"
install -Dm 644 "$srcdir/etoken.service" "$pkgdir/usr/lib/systemd/system/etoken.service"
install -Dm 644 "$srcdir/${path}/usr/share/eToken/shortcuts/SACMonitor.desktop" "$pkgdir/usr/share/applications/SACMonitor.desktop"
install -Dm 644 "$srcdir/${path}/usr/share/eToken/shortcuts/SACTools.desktop" "$pkgdir/usr/share/applications/SACTools.desktop"
install -Dm 644 "$srcdir/${path}/usr/share/eToken/shortcuts/icons/SACMonitor.png" "$pkgdir/usr/share/icons/hicolor/32x32/SACMonitor.png"
install -Dm 644 "$srcdir/${path}/usr/share/eToken/shortcuts/icons/SACTools.png" "$pkgdir/usr/share/icons/hicolor/32x32/SACTools.png"
}
