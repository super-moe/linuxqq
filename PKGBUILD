# Maintainer: Purofle <purofle@gmail.com>
# Contributor: Integral <integral@member.fsf.org>

pkgname=linuxqq
pkgver=3.2.13_29927
pkgrel=1
epoch=5
pkgdesc="New Linux QQ based on Electron"
arch=('x86_64' 'aarch64' 'loong64')
url="https://im.qq.com/${pkgname}"
license=('LicenseRef-QQ')
conflicts=("${pkgname}-nt-bwrap")
depends=('nss' 'alsa-lib' 'gtk3' 'gjs' 'at-spi2-core' 'libvips' 'openjpeg2' 'openslide')
optdepends=('libappindicator-gtk3: Allow QQ to extend a menu via Ayatana indicators in Unity, KDE or Systray (GTK+ 3 library).')
_md5_prefix=833d113c
_src_prefix="${pkgname}_${pkgver/_/-}"
source_x86_64=("https://dldir1.qq.com/qqfile/qq/QQNT/${_md5_prefix}/${_src_prefix}_amd64.deb")
source_aarch64=("https://dldir1.qq.com/qqfile/qq/QQNT/${_md5_prefix}/${_src_prefix}_arm64.deb")
source_loong64=("https://dldir1.qq.com/qqfile/qq/QQNT/${_md5_prefix}/${_src_prefix}_loongarch64.deb")
source=("${pkgname}.sh")
sha512sums=('f463c5cb3323b86d9ea312d75f1e53d064885dabde2d1d6a554e083e15b5ff7fc548a96670284e5e996456c7a2ce4a25e9acb80bf48459ea47a8813d62203cb4')
sha512sums_x86_64=('4f9d513127b126c0daa78d32bdb8cc4777a9d9e2bbd01bee39273039379692267dabab521edb6acd9660be86cdacb686dbcb10cc36acdb9858b8f8d2cdf68f16')
sha512sums_aarch64=('6b28cf9a00aab97a4304df1a8e16f6ad6b4d058cdf9b67f28faa5794fa9b5bfe7069707fd327cc9e18cd4fc022c4f1b812fd89d986ac13a06f90d403f2ecd6f0')
sha512sums_loong64=('ac5ad66711db2446218e4d555793d002459c877a80f6be9bcc8a2b0d990a78299c30d832ddc5c2a3471493bb038050372f27bee596b50f5c686919af170745a4')
options=('!strip' '!debug')

package() {
	echo "  -> Extracting the data.tar.xz..."
	bsdtar -xf data.tar.xz -C "${pkgdir}/"
	rm -f "${pkgdir}/opt/QQ/resources/app/libssh2.so.1" # Temporary Fix

	echo "  -> Installing..."
	# Launcher
	install -Dm755 "${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"

	# Launcher Fix
	sed -i '3s!/opt/QQ/qq!linuxqq!' "${pkgdir}/usr/share/applications/qq.desktop"

	# Icon Fix
	sed -i '6s!/usr/share/icons/hicolor/512x512/apps/qq.png!qq!' "${pkgdir}/usr/share/applications/qq.desktop"

	# License
	install -Dm644 "${pkgdir}/opt/QQ/LICENSE.electron.txt" -t "${pkgdir}/usr/share/licenses/${pkgname}/"
	install -Dm644 "${pkgdir}/opt/QQ/LICENSES.chromium.html" -t "${pkgdir}/usr/share/licenses/${pkgname}/"

	# Temporary Solution: Remove libvips which comes from package "linuxqq" itself
	rm -f "${pkgdir}/opt/QQ/resources/app/sharp-lib/libvips-cpp.so.42"
}
