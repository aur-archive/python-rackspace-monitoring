# Maintainer: Carl George <carl@cgtx.us>

_module1="rackspace-monitoring"
_ver1="0.6.4"
_module2="rackspace-monitoring-cli"
_ver2="0.6.7"

# Can't build rackspace-monitoring-cli on py3 until this is resolved.
# https://github.com/racker/rackspace-monitoring-cli/issues/59
#pkgname=("python-${_module1}" "python-${_module2}" "python2-${_module1}" "python2-${_module2}")
pkgname=("python-${_module1}" "python2-${_module1}" "python2-${_module2}")

# This variable can't be empty.  Override in each package function.
pkgver="0"

pkgrel="2"
arch=("any")
license=("Apache")
makedepends=("python-setuptools" "python2-setuptools")
source=("https://pypi.python.org/packages/source/${_module1:0:1}/${_module1}/${_module1}-${_ver1}.tar.gz"
	"https://pypi.python.org/packages/source/${_module2:0:1}/${_module2}/${_module2}-${_ver2}.tar.gz")

prepare() {
	cp -a "${srcdir}/${_module1}-${_ver1}"{,-python2}
	cp -a "${srcdir}/${_module2}-${_ver2}"{,-python2}
}

build() {
	# python 3
	cd "${srcdir}/${_module1}-${_ver1}"
	python setup.py build
	#cd "${srcdir}/${_module2}-${_ver2}"
	#python setup.py build
	# python 2
	cd "${srcdir}/${_module1}-${_ver1}-python2"
	python2 setup.py build
	cd "${srcdir}/${_module2}-${_ver2}-python2"
	python2 setup.py build
}

# python 3
package_python-rackspace-monitoring() {
	pkgver="${_ver1}"
	pkgdesc="Client library for Rackspace Cloud Monitoring"
	url="https://github.com/racker/${_module1}"
	depends=("python-apache-libcloud") # py3 version from aur
	cd "${srcdir}/${_module1}-${_ver1}"
	python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
#package_python-rackspace-monitoring-cli() {
#	pkgver="${_ver2}"
#	pkgdesc="Command Line Utility for Rackspace Cloud Monitoring"
#	url="https://github.com/racker/${_module2}"
#	depends=("python-rackspace-monitoring")
#	cd "${srcdir}/${_module2}-${_ver2}"
#	python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
#}

# python 2
package_python2-rackspace-monitoring() {
	pkgver="${_ver1}"
	pkgdesc="Client library for Rackspace Cloud Monitoring"
	url="https://github.com/racker/${_module1}"
	depends=("apache-libcloud") # py2 version from community
	cd "${srcdir}/${_module1}-${_ver1}-python2"
	python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
package_python2-rackspace-monitoring-cli() {
	pkgver="${_ver2}"
	pkgdesc="Command Line Utility for Rackspace Cloud Monitoring"
	url="https://github.com/racker/${_module2}"
	depends=("python2-rackspace-monitoring")
	cd "${srcdir}/${_module2}-${_ver2}-python2"
	python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}

sha256sums=('28b972d7fc829aa6e3c7c63c5c2e6ec3917436431d595cc122958dc14d09d3ad'
            '896ae25e8be2f237dfcdd99529350aeb43dfe4b8a61bdc8397434ab55ef9bd5c')
