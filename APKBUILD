pkgname=wayfire-git
_repo="https://github.com/WayfireWM/wayfire"
options="!check"
pkgver="_git"
pkgrel=0
provides='wayfire'
pkgdesc="Compiz-clone Wayland compositor"
url="https://wayfire.org"
arch="all !ppc64le !mips64" # blocked by wlroots
license="MIT"
makedepends="
	meson
	wlroots-dev
	glm-dev
	wf-config-dev
	cairo-dev
	libexecinfo-dev
	libxml2-dev
	wayland-protocols
	vulkan-headers
	doctest-dev
	doxygen
	xwayland
	xwayland-dev
	inotify-tools
	"
subpackages="$pkgname-dev"
source=""

prepare() {
    default_prepare
    cd "${srcdir}"
    git clone "${_repo}"
    cd "${pkgname}"
    git submodule update
}

build() {
    cd "${srcdir}/${pkgname}"
    abuild-meson \
	-Duse_system_wlroots=enabled \
	-Duse_system_wfconfig=enabled \
	. output
    meson compile ${JOBS:+--j ${JOBS}} -C output
}

package() {
    cd "${srcdir}/${pkgname}"
    DESTDIR="$pkgdir" meson install --no-rebuild -C output

    install -Dm644 wayfire.ini "$pkgdir"/usr/share/wayfire/wayfire.ini.default
}
