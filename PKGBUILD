# Maintainer: Michal S <michal[at]tar[dot]black>

pkgname=pkg-warner
pkgver=0.1.3
pkgrel=2
pkgdesc="Simple package manager warner tool for distribution developers"
arch=('x86_64')
url="https://github.com/crystal-linux/${pkgname}"
license=('GPL3')
source=("${pkgname}-${pkgver}::${url}/archive/v${pkgver}.tar.gz")
sha256sums=('c717ba88d946d719c6580a3580cd332a9853137d82a7d6bf4aa0bb79886bc6be')
makedepends=('cargo')

prepare() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    cargo fetch --locked --target "${CARCH}-unknown-linux-gnu"
}

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
        
    # These following envvars are Crystal-specific, please adjust for your own distro!
    export PKG_WARNER_PACKAGES="apt,apt-get,dnf,pkg,rpm,yum,zypper,eopkg"
    export PKG_WARNER_DISTRO="Crystal"
    export PKG_WARNER_PMAN="ame/pacman"
    
    cargo build --frozen --release
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    cargo run --frozen --release -- -ivd "${pkgdir}/usr/bin"
}
