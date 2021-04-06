# Maintainer: Mohammad Hadi Hosseinpour <hadi77ir@github.com>

_pkgbase=linux-virtfb
_reponame=linux-module-virtfb
pkgname=linux-virtfb-dkms
pkgver=r4.0de67b6
pkgrel=1
pkgdesc="Virtual framebuffer kernel module (DKMS)"
arch=('i686' 'x86_64' 'armv7')
url="https://github.com/hadi77ir/linux-module-virtfb"
license=('GPL2')
depends=('dkms')
conflicts=("${_pkgbase}")
source=("git+https://github.com/hadi77ir/${_reponame}.git"
        'dkms.conf')
md5sums=('SKIP' 'SKIP')

pkgver() {
  cd "${_reponame}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd ${_reponame}

  # Install
  make DESTDIR="${pkgdir}/usr" install

  cd ..

  # Copy dkms.conf
  install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@BUILT_MODULE@/virtfb/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Copy sources (including Makefile)
  cp -r ${_reponame}/* "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/
}
