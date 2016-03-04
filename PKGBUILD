# Maintainer: Benjamin Kammerl <benny@itws.de>

pkgname=apexctl-git
pkgver=0.0.1
pkgrel=1
pkgdesc="An utility to enable extra macro keys on Steelseries Apex keyboards. Latest GIT version."
url="https://github.com/tuxmark5/ApexCtl"
license=('GPL3')
depends=(libusb)
makedepends=(ghc cabal-install git pkg-config)
options=(!strip)
arch=('i686' 'x86_64')

source=()
md5sums=()

_gitroot="https://github.com/tuxmark5/ApexCtl.git"
_gitname=ApexCtl

build() {
    cd "${srcdir}"

    rm -rf "${_gitname}-build"

    if [ ! -d "${srcdir}/${_gitname}" ]; then
        msg "Cloning ..."
        git clone ${_gitroot} ${_gitname}
    else
        msg "Updating ..."
        cd ${_gitname} && git pull origin
    fi

    msg "Creating build dir ..."
    cd "${srcdir}"
    cp -rf "${_gitname}" "${_gitname}-build"
    cd "${_gitname}-build"

    msg "Install dependencies via cabal ..."
    cabal update
    cabal install usb cmdargs

    msg "Compiling ..."
    make
}

package() {
    cd "${srcdir}/${_gitname}-build"
    mkdir -p ${pkgdir}/usr/local/bin/ \
        ${pkgdir}/etc/X11/ \
        ${pkgdir}/etc/udev/hwdb.d/ \
        ${pkgdir}/etc/udev/rules.d/
    make INSTALL_ROOT="${pkgdir}" install
}
