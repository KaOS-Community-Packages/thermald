pkgname=thermald
_pkgname=thermal_daemon
pkgver=1.5.2
pkgrel=1
pkgdesc="The thermald daemon prevents machines from overheating"
arch=('x86_64')
url='https://github.com/01org/thermal_daemon'
license=('GPL2')
makedepends=('systemd')
depends=('dbus-glib' 'libxml2')
backup=('etc/thermald/thermal-conf.xml')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        'modules-load-thermald.conf')
sha256sums=('e44b3cdd8a3c385d32d093b6c0b50f5804daad1ed3f5ef16df24b7a3fa048064'
            '0155e1eb459306d251a5a049ffc6c11e144fa8caa75901ac5fa20bd52e05d515')
build() {
  cd "${_pkgname}-${pkgver}"
  ./autogen.sh
  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --localstatedir=/var \
              --sbindir=/usr/bin
  make
}

package() {
  cd "${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -Dm644 "${srcdir}/modules-load-thermald.conf" "${pkgdir}/usr/lib/modules-load.d/thermald.conf"

  # Remove Upstart related files
  rm -r "${pkgdir}/etc/init"
}
