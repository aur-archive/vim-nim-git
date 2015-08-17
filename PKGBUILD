# Maintainer: Andy Weidenbaum <archbaum@gmail.com>

pkgname=vim-nim-git
pkgver=20150510
pkgrel=1
pkgdesc="Nim language support for Vim"
arch=('any')
depends=('vim')
makedepends=('git')
groups=('vim-plugins')
url="https://github.com/zah/nim.vim"
license=('custom:vim')
source=(${pkgname%-git}::git+https://github.com/zah/nim.vim)
sha256sums=('SKIP')
provides=('vim-nim')
conflicts=('vim-nim')
install=vimdoc.install

pkgver() {
  cd ${pkgname%-git}
  git log -1 --format="%cd" --date=short | sed "s|-||g"
}

prepare() {
  cd ${pkgname%-git}

  msg 'Fixing Python version...'
  find . -type f -print0 | xargs -0 sed -i 's#/usr/bin/python#/usr/bin/python2#g'
  find . -type f -print0 | xargs -0 sed -i 's#/bin/python#/usr/bin/python2#g'
  find . -type f -print0 | xargs -0 sed -i 's#/usr/bin/env python#/usr/bin/env python2#g'
  find . -type f -print0 | xargs -0 sed -i 's#/bin/env python#/usr/bin/env python2#g'
}

package() {
  cd ${pkgname%-git}

  msg 'Installing docs...'
  install -Dm 644 README.markdown "$pkgdir/usr/share/doc/vim-nim/README.markdown"

  msg 'Installing dirs...'
  install -dm 755 "$pkgdir/usr/share/vim/vimfiles"
  for _dir in autoload compiler ftdetect ftplugin indent syntax; do
    cp -dpr --no-preserve=ownership $_dir "$pkgdir/usr/share/vim/vimfiles/$_dir"
  done

  msg 'Cleaning up pkgdir...'
  find "$pkgdir" -type d -name .git -exec rm -r '{}' +
}
