# Maintainer: Niels Martignène <niels.martignene@gmail.com>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Alessio 'mOLOk' Bolognino <themolok@gmail.com>
# Contributor: shamrok <szamrok@gmail.com>

pkgname=smplayer-tray-options
pkgver=14.9.0
pkgrel=1
pkgdesc="A complete front-end for MPlayer"
arch=('i686' 'x86_64')
url="http://smplayer.sourceforge.net/"
license=('GPL')
depends=('qt4' 'mplayer')
optdepends=('smplayer-themes: icon themes collection'
            'smplayer-skins: skin themes collection'
            'smtube: browse and play youtube videos')
provides=('smplayer')
conflicts=('smplayer')
install=smplayer.install
source=(http://downloads.sourceforge.net/sourceforge/smplayer/smplayer-$pkgver.tar.bz2
        'add-tray-options.patch'
        'disable-update-checker.patch')
sha256sums=('429ad4edd6df1fcedd5ea4fa2b024eb5a61c9412f52762e9d9a9c2245b7ddf13'
            'e614926c473a03eee89cf2477023c41d42e5c16d4f79de46d29ac31f4614d24f'
            '068066cf9bf0deeae215927f6a98c5aad9a46212dab4cc585da4d78eedef50a0')

prepare() {
  cd "smplayer-$pkgver"

  # Add tray options
  patch -Np0 < "$srcdir/add-tray-options.patch"

  # Don't check for updates
  patch -Np1 < "$srcdir/disable-update-checker.patch"
}

build() {
  cd "smplayer-$pkgver"
  make PREFIX=/usr QMAKE=qmake-qt4 LRELEASE=lrelease-qt4 \
    DOC_PATH="\\\"/usr/share/doc/smplayer\\\"" \
    QMAKE_OPTS=DEFINES+=NO_DEBUG_ON_CONSOLE
}

package() {
  cd "smplayer-$pkgver"
  make DOC_PATH=/usr/share/doc/smplayer \
    DESTDIR="$pkgdir" PREFIX="/usr" install
}
