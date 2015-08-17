# Contributor: Mike Redd <mredd -at- zerotuezero dot com>
# Maintainer: Mike Redd <mredd -at- zerotuezero dot com>

pkgname=rsstail.py-git
pkgver=20140804
pkgrel=1
pkgdesc="Rsstail is a command-line syndication feed monitor with behaviour similar to tail -f. Rsstail python/feedparser is inspired by rsstail C/libmrss, but provides more customizable output formatting and additional features."
arch=('i686' 'x86_64')
url="http://www.vanheusden.com/rsstail/"
license=('BSD')
depends=('python2-feedparser' 'python2')
makedepends=('git')
optdepends=('clide: a program that will colorize ascii text on the command line'
            'multitail: lets you view one or multiple files like the original tail program.')
install=
conflicts=('rsstail')
replaces=('rsstail')
provides=('rsstail')
source=("git+https://github.com/gvalkov/rsstail.py.git")

md5sums=('SKIP')
sha256sums=('SKIP')

_gitroot="git://github.com/gvalkov/rsstail.py.git"
_gitname="rsstail.py"

build() {
  cd $srcdir
  # checkout
  if [ -d $srcdir/$_gitname ] ; then
     cd $_gitname && git pull origin
  else
     git clone --depth 1 $_gitroot $_gitname && cd $_gitname
  fi
  cd $srcdir/$_gitname
  # reset the version tag
  git reset --hard HEAD $versiontag
  # replace python with python2
  sed -i 's/env python/env python2/' setup.py
  sed -i 's/env python/env python2/' compgen.py
  sed -i 's/env python/env python2/' rsstail/formatter.py
  sed -i 's/env python/env python2/' rsstail/main.py
  sed -i 's/env python/env python2/' rsstail/version.py
  sed -i 's/env python/env python2/' tests/test_formatter.py
  sed -i 's/env python/env python2/' tests/test_script.py
}

package() {
  cd $srcdir/$_gitname
  python2 setup.py install --prefix=/usr --root="$pkgdir" || return 1
  # install license
  install -Dm655 LICENSE $pkgdir/usr/share/licenses/$_gitname/LICENSE
}

# vim:set ts=2 sw=2 et:
