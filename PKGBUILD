pkgname=foundationdb-bin
pkgver=7.1.43
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
	'9df1c7043fd12d53378cbb96ecc59261225c2ff59aed76159436ebc7102b1276'
	'732de9475c24f46b29ebb52cccb75fc22f56b5984ae3e04af843b65753c57499'
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
