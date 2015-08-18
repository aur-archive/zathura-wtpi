# $Id: PKGBUILD 90594 2013-05-13 10:03:23Z spupykin $
# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: ML <neldoreth>
# Contributor: Shizeeg Unadequatov <shizeeque@gmail.com>

pkgname=zathura-wtpi
pkgver=0.2.3
pkgrel=3
pkgdesc="a document viewer (with window-title-curpage option)"
arch=('i686' 'x86_64')
url="http://pwmt.org/projects/zathura/"
license=('custom')
depends=('girara-gtk2' 'sqlite' 'desktop-file-utils')
makedepends=('python2-docutils')
optdepends=('zathura-djvu' 'zathura-pdf-poppler' 'zathura-pdf-mupdf' 'zathura-ps')
conflicts=('zathura' 'zathura-git')
provides=('zathura')
install=zathura.install
source=(http://pwmt.org/projects/zathura/download/zathura-$pkgver.tar.gz
	bash-completion
	zathura-window-curpage.patch
	zathura-statusbar-show.patch)

md5sums=('c0265fd9fa64a37b01d729efb75a7c32'
         'cac20c37f0e77ba62a8138788f4ccabb'
         '1b2b63cc9d22e71a21a3091d9ddebc1d'
         'df27d0223945ba3d949fa4a377eb3294')

prepare() {
  cd $srcdir/zathura-$pkgver
  cat $srcdir/zathura-window-curpage.patch | patch -p1
  cat $srcdir/zathura-statusbar-show.patch | patch -p1
}

build() {
  cd $srcdir/zathura-$pkgver
  sed -i 's/rst2man/&2/' config.mk
  make ZATHURA_GTK_VERSION=2
}

package() {
  cd $srcdir/zathura-$pkgver
  make install DESTDIR=$pkgdir ZATHURA_GTK_VERSION=2
  install -D -m664 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm0644 $srcdir/bash-completion $pkgdir/usr/share/bash-completion/completions/zathura
}
