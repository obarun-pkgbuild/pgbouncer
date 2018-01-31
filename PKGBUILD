# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/pgbouncer
#						Maintainer: Dan McGee <dan@archlinux.org>

pkgname=pgbouncer
pkgver=1.8.1
pkgrel=2
pkgdesc="A lightweight connection pooler for PostgreSQL"
arch=(x86_64)
url='https://pgbouncer.github.io/'
license=('BSD')
depends=('libevent>=2.0' 'c-ares' 'pam')
makedepends=('asciidoc' 'xmlto')
checkdepends=('postgresql-libs')
backup=('etc/pgbouncer/pgbouncer.ini'
        'etc/logrotate.d/pgbouncer')
install=${pkgname}.install
source=(https://pgbouncer.github.io/downloads/files/${pkgver}/pgbouncer-${pkgver}.tar.gz
		pgbouncer.ini
        pgbouncer.logrotate
        pgbouncer.tmpfiles.conf)
sha256sums=('de36b318fe4a2f20a5f60d1c5ea62c1ca331f6813d2c484866ecb59265a160ba'
            '4f30e4a3eb76acdd233ebc7dd099dff6976299ba958e40a8429b74112e804b05'
            '8da38746d9c9dfc2433a8cfe22fdaf517e14492672d09e3c48cd4745fc03e9bd'
            '476ea0400ba063e932a58f1f49ae401d65b22add521894872c09ec6985e0960d'
            '46d2d1c421ccd9893af4f6fde28d796b7910d2385efd3e27cca118d8e484ca7b')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

build() {
  cd "$pkgname-$pkgver"
  ./configure --prefix=/usr --disable-debug --with-pam
  make
}

check() {
  cd ${pkgname}-${pkgver}
  make -C test run_test
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="${pkgdir}" install
  install -D -m 0644 NEWS.rst -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -D -m 0644 COPYRIGHT "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -D -m 0644 ../pgbouncer.ini "$pkgdir/etc/pgbouncer/pgbouncer.ini"
  install -D -m 0644 ../pgbouncer.logrotate "$pkgdir/etc/logrotate.d/pgbouncer"
  install -D -m 0644 ../pgbouncer.tmpfiles.conf "$pkgdir/usr/lib/tmpfiles.d/pgbouncer.conf"
  install -d "$pkgdir/var/log/pgbouncer"
}
