# Maintainer: Sébastien Luttringer

pkgname=archivetools-git
pkgver=2+4+gd954a96
pkgrel=1
pkgdesc='Arch Linux Archive Tools'
arch=('any')
url='https://github.com/archlinux/archivetools'
license=('GPL2')
depends=('rsync' 'hardlink' 'xz' 'util-linux' 'systemd')
makedepends=('git')
backup=('etc/archive.conf')
provides=('archivetools')
conflicts=('archivetools')
source=(${pkgname}::"git+https://github.com/archlinux/archivetools.git")
md5sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags|sed 's|-|+|g'|sed -E 's|v?(.*)|\1|'
}

package() {
  cd $pkgname
  install -Dm644 archive.conf "$pkgdir/etc/archive.conf"
  install -Dm755 archive.sh "$pkgdir/usr/bin/archive"
  # systemd stuff
  install -Dm644 archive.sysusers "$pkgdir/usr/lib/sysusers.d/archive.conf"
  install -Dm644 archive.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/archive.conf"
  for _p in archive.{timer,service} archive-hardlink.{timer,service}; do
    install -Dm644 $_p "$pkgdir/usr/lib/systemd/system/$_p"
  done
}

# vim:set ts=2 sw=2 et:
