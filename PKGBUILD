# Maintainer: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Dave Reisner <d@falconindy.com>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: godane <slaxemulator@gmail.com.com>
# Contributor: Andres Perera <aepd87@gmail.com>

pkgname=pacman
pkgver=99.0.0
pkgrel=1
pkgdesc="A library-based package manager with dependency support"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64' 'amd64')
url="https://github.com/icy/pacapt"
license=('GPL')
#depends=
#         'pacman-mirrorlist')
optdepends=('libjson-perl' 'shellcheck')
#'pacman-contrib: various helper utilities'
#            'perl-locale-gettext: translation support in makepkg-template')
makedepends=('git' 'bash')
checkdepends=('bash' 'fakechroot')
provides=("pacman=${pkgver%.*.*}")
conflicts=('pacman')
#backup=("etc/pacman.conf"
#        "etc/makepkg.conf")
options=('emptydirs' 'strip' 'debug')
source=("git+https://github.com/icy/pacapt.git")
sha256sums=('SKIP')

prepare() {
		[[ -d "$pkgname-$pkgver" ]] && rm -rf "$pkgname-$pkgver"
		mv pacapt "$pkgname-$pkgver"
    cd "$pkgname-$pkgver"
    patch --forward -i ../../pacman.patch
}

pkgver() {
  echo "$pkgver"
}

build() {
  cd "$pkgname-$pkgver"
	make POSIX pacapt.dev VERSION="$pkgver" 
}

#check() {
#	cd "$pkgname-$pkgver"
#	mkdir -p tests/tmp/
#	sh ./bin/gen_tests.sh < tests/dpkg.txt > tests/tmp/test.sh
#  cd tests/tmp/
#	sh ./test.sh
#
#  env BINDIR=/usr/local/bin make -C .. test
#}

package() {
  cd "$pkgname-$pkgver"

  sudo make install.dev VERSION="$pkgver"
}

# vim: set ts=2 sw=2 et:
