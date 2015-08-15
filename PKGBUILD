# Maintainer: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>

pkgname=django-1.4
pkgver=1.4.20
pkgrel=1
pkgdesc="A high-level Python Web framework that encourages rapid development and clean design"
arch=('any')
license=('BSD')
url="http://www.djangoproject.com/"
depends=('python2')
makedepends=('python2-setuptools')
optdepends=('mysql-python: for MySQL backend'
            'python2-psycopg2: for PostgreSQL backend')
conflicts=('python2-django')
provides=('python2-django=1.4.20')
source=(https://www.djangoproject.com/m/releases/1.4/Django-$pkgver.tar.gz)
sha256sums=('58ac719464c4c8b13d664ded6770450602528bf4c36f9fd5daabdae8d410ebb1')

build() {
  cd "${srcdir}"/Django-$pkgver
  python2 setup.py build
}

package() {
  cd "${srcdir}"/Django-$pkgver
  python2 setup.py install --root="${pkgdir}" --optimize=1

  install -Dm644 extras/django_bash_completion \
    "${pkgdir}"/usr/share/bash-completion/completions/django-admin.py
  ln -s django-admin.py \
    "${pkgdir}"/usr/share/bash-completion/completions/manage.py

  find "${pkgdir}"/usr/lib/python2.7/site-packages/django/ -name '*.py' | \
    xargs sed -i "s|#!/usr/bin/env python$|#!/usr/bin/env python2|"

  install -Dm644 LICENSE "${pkgdir}"/usr/share/licenses/$pkgname/LICENSE
}
