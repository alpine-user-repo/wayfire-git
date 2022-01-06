_pkgname=wayfire
repo="https://github.com/WayfireWM/wayfire"
pkgname="${_pkgname}-git"
options="!check"
pkgver="_git"
pkgrel=0
provides='${_pkgname}=_git'
pkgdesc="Compiz-clone Wayland compositor"
url="https://wayfire.org"
arch="all !ppc64le !mips64" # blocked by wlroots
license="MIT"
makedepends="
	meson
	glm-dev
	cairo-dev
	libexecinfo-dev
	vulkan-headers
	doctest-dev
	doxygen
	inotify-tools-dev
	eudev-dev
	libcap-dev
	libinput-dev
	libseat-dev
	libxcb-dev
	libxkbcommon-dev
	mesa-dev
	pixman-dev
	wayland-dev
	wayland-protocols
	xcb-util-image-dev
	xcb-util-renderutil-dev
	xcb-util-wm-dev
	xkeyboard-config
	xwayland-dev
	ninja
	cmake
	pango-dev
	libevdev-dev
	libxml2-dev
	linux-headers
	"
subpackages="$pkgname-dev"
source=""
builddir="${srcdir}/${_pkgname}"

prepare() {
    default_prepare
    cd "${srcdir}"
    git clone "${repo}"
    cd "${_pkgname}"
    git submodule update
}

build() {
    cd "${builddir}"
    abuild-meson \
	-Duse_system_wlroots=disabled \
	-Duse_system_wfconfig=disabled \
	. output
    meson compile ${JOBS:+--j ${JOBS}} -C output
}

package() {
    cd "${builddir}"
    DESTDIR="$pkgdir" meson install --no-rebuild -C output

    install -Dm644 wayfire.ini "$pkgdir"/usr/share/wayfire/wayfire.ini.default
}
