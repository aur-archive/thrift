# Contributor: Byron Clark <byron@theclarkfamily.name>
# based on thrift-git PKGBUILD
pkgname=thrift
pkgver=0.9.1
pkgrel=1
pkgdesc="Scalable cross-language services framework for IPC/RPC"
arch=(i686 x86_64)
url="http://thrift.apache.org/"
license=(APACHE)
depends=(boost-libs)
makedepends=(boost java-environment apache-ant apache-ant-maven-tasks python2 php perl perl-bit-vector perl-class-accessor glib2)
optdepends=('python2: to use Python bindings'
            'java-environment: to use Java bindings'
            'php: to use PHP bindings'
            'perl: to use Perl bindings'
            'perl-bit-vector: to use Perl bindings'
            'perl-class-accessor: to use Perl bindings'
            'glib2: to use C (glib) bindings')
options=(!emptydirs !makeflags)
source=(http://www.apache.org/dist/$pkgname/$pkgver/$pkgname-$pkgver.tar.gz
        maven-repo-path.patch)
md5sums=('d2e46148f6e800a9492dbd848c66ab6e'
         'bfcb3b12a8c07d5d0d9e96a7e712a74c')

build() {
  cd $srcdir/$pkgname-$pkgver

  patch -p1 -i $srcdir/maven-repo-path.patch

  # apache-ant is not installed in a normal path location
  . /etc/profile.d/apache-ant.sh

  CFLAGS="${CFLAGS} -fno-strict-aliasing"
  PYTHON=/usr/bin/python2 GCOV_CFLAGS="${CFLAGS}" ./configure --prefix=/usr --without-ruby --without-php --without-cpp --without-ocalm --without-haskell
  make
}

package() {
  cd $srcdir/$pkgname-$pkgver

  make DESTDIR=$pkgdir install

  # ViM syntax file
  install -d -m 0755 $pkgdir/usr/share/vim/vimfiles/syntax
  install -m 0644 contrib/thrift.vim $pkgdir/usr/share/vim/vimfiles/syntax

  # Fix lib installation directory
  mv "$pkgdir/usr/local/lib"/* "$pkgdir/usr/lib"
  rmdir "$pkgdir/usr/local/lib"
}

# vim:set ts=2 sw=2 et:
