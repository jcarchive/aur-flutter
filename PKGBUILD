# Maintainer: Jose C.

pkgname=flutter
pkgver=3.0.1
pkgrel=1
pkgdesc="Is an open source framework by Google for building beautiful, natively compiled, multi-platform applications from a single codebase."
arch=('x86_64')
options=('!strip')
url="https://flutter.dev/"
license=('custom')
provides=('flutter')
conflicts=('flutter')
install="$pkgname.install"

_filename="flutter_linux_$pkgver-stable.tar.xz"
_fileextract="flutter"

source=("https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_$pkgver-stable.tar.xz")

sha256sums=( 'fe088c6c399d3bf6958171cec1dfdb387bacb1b643413fa07e6c353fad80adc1')
package() {
    cd $srcdir

    #Clean uneeded files base on https://dart.dev/guides/libraries/private-files
    find -name .dart_tool -type d -exec rm -fr {} +
    find -name .packages  -type f -exec rm -fr {} +
    find -name build -type d -exec rm -fr {} +
    find -name pubspec.lock -exec rm -fr {} +

    find -wholename doc/api -type d -exec rm -fr {} +

    find -name *.iml -type f -exec rm -f {} +
    find -name *.ipr -type f -exec rm -f {} +
    find -name *.iws -type f -exec rm -f {} +
    find -name .idea -type d -exec rm -fr {} +

    find -name .DS_Store -type f -exec rm -f {} +

    #Create directories with permission rwxr-xr-x
    install -m755 -d "$pkgdir/usr/share" "$pkgdir/usr/bin"
    install -Dm644 "$srcdir/$_fileextract/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

    #Copy files to pkg destination
    cp -r "$srcdir/$_fileextract" "$pkgdir/usr/share/$pkgname"
    chown -R root:root "$pkgdir/usr/share/$pkgname"
    chmod -R a+rw "$pkgdir/usr/share/$pkgname/bin/cache"
    chmod -R a+rw "$pkgdir/usr/share/$pkgname/version"

    ln -s "/usr/share/$pkgname/bin/flutter" "$pkgdir/usr/bin/flutter"
}
