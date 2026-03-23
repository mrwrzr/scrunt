# Maintainer: github.com/mrwrzr
# GNU GPL v3.0

pkgname=scrunt
pkgver=0.1.0
pkgrel=1
pkgdesc="automated all-in one update script"
arch=('any')
url="https://github.com/mrwrzr/scrunt"
license=('GPLv3')
depends=('bash' 'dialog')
optdepends=('fastfetch' 'timeshift' 'snapper')
source=("$pkgname-$pkgver.tar.gz::https://github.com/mrwrzr/scrunt/archive/v$pkgver.tar.gz")
sha256sums=('SKIP')

package() {
  cd "$srcdir/$pkgname-$pkgver"

  install -Dm755 scrunt "$pkgdir/usr/bin/scrunt"
  install -Dm755 scrunt-wizard "$pkgdir/usr/bin/scrunt-wizard"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
