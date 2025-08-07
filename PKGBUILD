pkgname=foundationdb-bin-sighol
pkgver=7.3.69
pkgrel=1
pkgdesc="FoundationDB is a scalable, fault-tolerant, ordered key-value store with full ACID transactions. This package contains the server and client."
arch=('x86_64')
url="https://www.foundationdb.org"
license=('Apache 2.0')
groups=('foundationdb')
depends=('glibc>=2', 'coreutils>=8', 'tar>=1')
options=('!strip' 'emptydirs')
install=${pkgname}.install
# Remove DLAGENTS once apple can fix their stuff https://bbs.archlinux.org/viewtopic.php?id=262737
DLAGENTS=("https::/usr/bin/curl -Lk -o %o %u")
source_x86_64=(
	"https://github.com/apple/foundationdb/releases/download/${pkgver}/foundationdb-server-${pkgver}-${pkgrel}.el7.x86_64.rpm"
	"https://github.com/apple/foundationdb/releases/download/${pkgver}/foundationdb-clients-${pkgver}-${pkgrel}.el7.x86_64.rpm"
)
sha256sums_x86_64=(
	'bc600a412c0bd4f7b884fc6955652341a49bb21a4a80f4c6157c41bd5dcccef3'
	'8678144b4433e24bd4f82c64cdbcf7c0b89ae66449dfbb95b9ce77a69faf7b7e'
)

package(){
	# Server
	mkdir -p "${pkgdir}/usr/lib"
	mkdir -p "${pkgdir}/etc"
	mkdir -p "${pkgdir}/usr"

	cp -r "${srcdir}/usr/lib" "${pkgdir}/usr"
	cp -r "${srcdir}/etc" "${pkgdir}/"
	cp -r "${srcdir}/var" "${pkgdir}/"
	cp -r "${srcdir}/lib" "${pkgdir}/usr"

	cp -r "${srcdir}/usr" "${pkgdir}/"
	mv "${pkgdir}"/usr/sbin/* "${pkgdir}/usr/bin"
	rmdir "${pkgdir}"/usr/sbin/

	sed -i 's_/usr/sbin_/usr/bin_g' "${pkgdir}/etc/foundationdb/foundationdb.conf"

	# FDBCli
	mv "${pkgdir}"/usr/lib64/* "${pkgdir}/usr/lib"
	rmdir "${pkgdir}"/usr/lib64/
}

post_remove() {
	rm -rf /var/lib/foundationdb
	rm -rf /var/log/foundationdb
	rm -rf /etc/foundationdb
}
