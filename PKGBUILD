# Maintainer: Lucas Declercq <lucas.declercq@hoohoot.org>
pkgname=f5epi
pkgver=7230.2022.0711.1
pkgrel=1
pkgdesc='Endpoint inspection application. It provide capabilities to check machines software processes and files'
arch=('x86_64')
source=('LICENSE')
source_x86_64=("linux_${pkgname}-${pkgver}-${pkgrel}.${CARCH}.rpm::https://vpn.f5.com/public/download/linux_${pkgname}.${CARCH}.rpm")
md5sums=('2508fc5e24d46163844dba9534fe7924')
md5sums_x86_64=('bab31dbf141058368f259d70e23e5388')
sha256sums=('a8f4b5d965dc0279dd5173109892251ce5d107d9912836e6d83a9b6896eb19a1')
sha256sums_x86_64=('c19c4e179c334b3add6eba64b3feb9c749c0c6265ef76cfb392d0e4793a226c8')
depends=(openssl qt5-base qt5-webkit)
provides=("${pkgname}")
url='https://support.f5.com/csp/article/K32311645#link_04_04'
license=('commercial')

package() {
    (
    cd "${srcdir}/opt/f5/epi"

    install -Dm644 "com.f5.${pkgname}.desktop" "${pkgdir}/usr/share/applications/com.f5.${pkgname}.desktop"
    install -Dm644 "com.f5.${pkgname}.service" "${pkgdir}/usr/share/dbus-1/services/com.f5.${pkgname}.service"
    install -dm755 "${pkgdir}/usr/bin/"

    for executable in $pkgname f5PolicyServer; do
        ln -s "/opt/f5/epi/${executable}" "${pkgdir}"/usr/bin/${executable}
    done

    # Use system Qt libraries
    for library in lib/*.so.*; do
        ln -sf "/usr/${library%%.so.*}.so" "$library"
    done

    # Use system Qt libraries
    for plugin in platforms/*.so; do
        ln -sf "/usr/lib/qt/plugins/${plugin}" "$plugin"
    done

    for resolution in 16 24 32 48 64 96 128 256 512 1024; do
        install -Dm644 "logos/${resolution}x${resolution}.png" \
                        "${pkgdir}/usr/share/icons/hicolor/${resolution}x${resolution}/apps/${pkgname}.png"
    done
    )
    install -Dm644 'LICENSE' "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    cp -a opt "${pkgdir}"
}

