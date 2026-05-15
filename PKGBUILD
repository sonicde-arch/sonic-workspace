# Maintainer: artist for XLibre <artist4xlibre@proton.me>

pkgbase=sonic-workspace
pkgname=(sonic-workspace sonic-x11-session)
pkgver=6.6.5
_pkgtag="${pkgver}"
pkgrel=1
pkgdesc='SonicDE workspace components'
arch=(x86_64)
url='https://github.com/Sonic-DE/sonic-workspace'
license=(LGPL-2.0-or-later)
depends=(accountsservice
         appstream-qt
         dbus
         fontconfig
         freetype2
         gcc-libs
         glibc
         icu
         kactivitymanagerd
         karchive
         kauth
         kbookmarks
         kcmutils
         kcolorscheme
         kcompletion
         kconfig
         kconfigwidgets
         kcoreaddons
         kcrash
         kde-cli-tools
         kdeclarative
         kded
         kdbusaddons
         kguiaddons
         kholidays
         ki18n
         kiconthemes
         kidletime
         kio
         kio-extras
         kio-fuse
         kirigami
         kirigami-addons
         kitemmodels
         kjobwidgets
         knewstuff
         knighttime
         knotifications
         knotifyconfig
         kpackage
         kparts
         kpipewire
         krunner
         kquickcharts
         kservice
         kstatusnotifieritem
         ksvg
         ksystemstats
         ktexteditor
         ktextwidgets
         kuserfeedback
         kwallet
         kwayland
         kwidgetsaddons
         kxmlgui
         layer-shell-qt
         libcanberra
         libice
         libkexiv2
         libqalculate
         libsm
         libx11
         libxau
         libxcb
         libxcrypt
         libxcursor
         libxfixes
         libxft
         libxtst
         milou
         ocean-sound-theme
         plasma-activities
         plasma-activities-stats
         plasma5support
         prison
         qt6-5compat
         qt6-base
         qt6-declarative
         qt6-location
         qt6-positioning
         qt6-svg
         qt6-tools # for qdbus
         qt6-virtualkeyboard
         sh
         solid
         sonic-frameworks-keybind
         sonic-frameworks-windowsystem
         sonic-interface-libraries
         sonic-screenlocker
         sonic-sysguard-library
         sonic-win
         systemd-libs
         wayland
         xcb-util
         xcb-util-cursor
         xcb-util-image
         xorg-xmessage
         xorg-xrdb
         xorg-xwayland
         zlib)
makedepends=(baloo
             extra-cmake-modules
             git
             kdoctools
             networkmanager-qt
             phonon-qt6
             plasma-wayland-protocols
             qcoro)
groups=(plasma)
source=("$pkgname-${pkgver}.tar.gz::${url}/archive/refs/tags/${_pkgtag}.tar.gz")
#source=("git+${url}.git#tag=${_pkgtag}")
sha256sums=('d67c6585d2c4ed5e4ebb8b8956955997532c5577c4c859e011f09daab2417093')
validpgpkeys=('E0A3EB202F8E57528E13E72FD7574483BB57B18D'  # Jonathan Esk-Riddell <jr@jriddell.org>
              '0AAC775BB6437A8D9AF7A3ACFE0784117FBCE11D'  # Bhushan Shah <bshah@kde.org>
              'D07BD8662C56CB291B316EB2F5675605C74E02CF'  # David Edmundson <davidedmundson@kde.org>
              '1FA881591C26B276D7A5518EEAAF29B42A678C20') # Marco Martin <notmart@gmail.com>

build() {
  #cmake -B build -S $pkgname \
  cmake -B build -S $pkgname-$pkgver \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DGLIBC_LOCALE_GEN=OFF \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package_sonic-workspace() {
  optdepends=('appmenu-gtk-module: global menu support for some GTK3 applications'
            'baloo: Baloo search runner'
            'discover: manage applications installation from the launcher'
            'kdepim-addons: displaying PIM events in the calendar'
            'kwayland-integration: Wayland integration for Qt5 applications'
            # 'kwin-x11: X session window manager'
            'networkmanager-qt: IP based geolocation'
            'plasma-workspace-wallpapers: additional wallpapers'
            'plasma5-integration: use Plasma settings in Qt5 applications'
            'xdg-desktop-portal-gtk: sync font settings to Flatpak apps')
  depends+=(sonic-x11-session plasma-integration) # Declare runtime dependency here to avoid dependency cycles at build time
  conflicts=(plasma-workspace plasma-wayland-session)
  provides=(plasma-workspace)
  groups=(sonicde)
  options=('!debug')

  DESTDIR="$pkgdir" cmake --install build

  rm -r "$pkgdir"/usr/share/xsessions/plasmax11.desktop
}


package_sonic-x11-session() {
  pkgdesc='Plasma X11 session, sonic edition, for XLibre'
  depends=(sonic-workspace)
  provides=(plasma-x11-session)
  conflicts=(plasma-x11-session)
  groups=(sonicde)

  install -Dm644 build/login-sessions/plasmax11.desktop -t "$pkgdir"/usr/share/xsessions
}
