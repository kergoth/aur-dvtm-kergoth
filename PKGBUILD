# Maintainer: Sean Haugh <seanphaugh@gmail.com>
# Contributor: Frank Lenormand <lenormf@gmail.com>
# Contributor: Christopher Larson <kergoth@gmail.com>
_pkgname=dvtm
_owner=kergoth
pkgname=dvtm-$_owner
pkgver=0.15.89.g299e836
pkgrel=1
pkgdesc='Dynamic virtual terminal manager'
arch=('i686' 'x86_64')
url="https://github.com/$_owner/$_pkgname"
license=('MIT')
depends=('sh')
makedepends=('git')
provides=("$_pkgname=$pkgver-$pkgrel")
conflicts=('dvtm')
source=("git+https://github.com/$_owner/$_pkgname#branch=$_owner")
md5sums=('SKIP')

pkgver() {
	cd "$_pkgname"
	git describe --long | sed 's/^v//; s/-/./g'
}

prepare() {
	cd "$_pkgname"
	[[ -e "$srcdir/config.h" ]] && cp "$srcdir/config.h" .

	sed -i"" 's/CFLAGS =/CFLAGS +=/' config.mk
}

build() {
	cd "$_pkgname"
	make
}

package() {
	cd "$_pkgname"
	make PREFIX=/usr DESTDIR="$pkgdir" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

	msg "Removing /usr/share/terminfo for compatibility with ncurses..."
	rm -rv "$pkgdir/usr/share/terminfo"
}
# vim: set ts=2 sw=2 noet:
