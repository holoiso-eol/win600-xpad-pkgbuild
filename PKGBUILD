# Maintainer: Antonis G. <capoiosct at gmail dot com>

_pkgname='xpad'
pkgname=win600-xpad-dkms
pkgver="6.3.7.snapshot$(date +%Y%m%d.%H%M)"
pkgrel='2'
pkgdesc="Driver for the Anbernic Win600 controller edits"
arch=('i686' 'x86_64')
url="https://github.com/theVakhovskeIsTaken/anbernic-win600-dkms"
license=('GPL2')
install="${pkgname}.install"
depends=('dkms')
makedepends=('git')
conflicts=("${_pkgname}-dkms")
source=("${pkgname}::git+https://github.com/theVakhovskeIsTaken/anbernic-win600-dkms"
        "xpad.conf"
        "90-rebuild-dkms-win600.hook"
        "${pkgname}.install")
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

package() {
    mkdir -p "${pkgdir}/etc/pacman.d/hooks"
    cp "${srcdir}/90-rebuild-dkms-win600.hook" "${pkgdir}/etc/pacman.d/hooks"
    ls -la
    sed -i "s/drvpkgver/${pkgver}/g" "${pkgdir}/etc/pacman.d/hooks/90-rebuild-dkms-win600.hook"
    # install depmod config file so our driver gets higher priority than the intree module
    install -dm 755 "$pkgdir/etc/depmod.d"
    install -m 644 "$srcdir/xpad.conf" "$pkgdir/etc/depmod.d"

    cd "$srcdir/$pkgname"
    install -dm 755 "${pkgdir}/usr/src/${_pkgname}-${pkgver}"
    install -m 644 -T xpad.c "${pkgdir}/usr/src/${_pkgname}-${pkgver}/xpad.c"
    install -m 644 -T Makefile "${pkgdir}/usr/src/${_pkgname}-${pkgver}/Makefile"
    install -m 644 -T dkms.conf "${pkgdir}/usr/src/${_pkgname}-${pkgver}/dkms.conf"
}
