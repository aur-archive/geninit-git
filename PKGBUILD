# Maintainer: Dave Reisner <d@falconindy.com>

pkgname=geninit-git
pkgver=20110516
pkgrel=1
pkgdesc="a modular initramfs creation utility"
arch=('i686' 'x86_64')
url="http://github.com/falconindy/geninit"
license=('MIT')
depends=('coreutils' 'bash' 'libarchive' 'file' 'findutils' 'grep'
         'module-init-tools' 'mkinitcpio-busybox' 'udev>=168')
makedepends=('sed' 'git')
optdepends=('lzop: LZO compression')
conflicts=('geninit')
provides=('geninit')
backup=(etc/geninit.conf)

_gitroot="git://github.com/falconindy/geninit.git"
_gitname="geninit"

build() {
  msg "Connecting to GIT server...."

  if [[ -d $_gitname ]] ; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  make
}

package() {
  make -C "$srcdir/$_gitname-build" PREFIX=/usr DESTDIR="$pkgdir" install
}

# vim: ft=sh syn=sh et
