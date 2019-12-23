---
title: Vim
description: 
published: true
date: 2019-12-23T14:33:34.793Z
tags: 
---

# Vim

## Installation

- Get the PKGBUILD from the official archlinux's repository. See : 

[archlinux.fr](https://wiki.archlinux.fr/Pacman#R.C3.A9cup.C3.A9rer_les_sources_d.27un_paquet)

- Modify PKGBUILD eg:

```shell
pkgbase=vim
pkgname=('vim' 'vim-runtime')
pkgver=8.1.2268
_versiondir=81
pkgrel=2
pkgdesc='Vi Improved, a highly configurable, improved version of the vi text editor'
url='https://www.vim.org'
arch=('x86_64')
license=('custom:vim')
makedepends=('glibc' 'libgcrypt' 'gpm' 'python2' 'python' 'ruby' 'libxt' 'gtk3' 'lua'
             'gawk' 'tcl' 'pcre' 'zlib' 'libffi' 'libcanberra')
source=(https://github.com/vim/vim/archive/v${pkgver}/${pkgbase}-${pkgver}.tar.gz
        vimrc
        archlinux.vim
        vimdoc.hook)
sha256sums=('bca27fc5bfda44cc40c383890379789fcb432873d223861c42f2f581556a860e'
            'b16e85e457397ab2043a7ee0a3c84307c6b4eac157fd0b721694761f25b3ed5b'
            'cc3d931129854c298eb22e993ec14c2ad86cc1e70a08a64496f5e06559289972'
            '7095cafac21df7aa42749d6864d1c0549fe65771d8edda3102c931c60782b6b9')
sha512sums=('00ade0a024c3eb39829ed79345fc13ee0b7fc6163fe71968c360ff6c05e3302c2d1b7bce1c5e934f24ff0f9911ea25baa6e75dc2d1548d5fb5f8e97ed6869659'
            '4b5bed0813f22af9e158ea9aa56a4a9862dd786ba2d201f20159ccf652da6190164aaed0b6b7217d578f7b25c33a8adcc307bfcf3caa8d173a7ff29e2a00fee7'
            'fe091d289d876f45319c898f6021ef86d6a238b540c225a279c46efc5c36fa7d868cd0cee73a111811c4be90df160f85340bb251be3a437727dbe5c699950363'
            '1e06e981691b17662fd0fddac5c00c87c920d1b4a1cbb6191c42d57cc40b00af12710e26b22fcfc0901bb8142b15f6a04aa65cec2d9b3bb9d5a06cb650d3ab9c')

prepare() {
  (cd vim-${pkgver}/src￼

    # define the place for the global (g)vimrc file (set to /etc/vimrc)
    sed -i 's|^.*\(#define SYS_.*VIMRC_FILE.*"\) .*$|\1|' feature.h
    sed -i 's|^.*\(#define VIMRC_FILE.*"\) .*$|\1|' feature.h
    autoconf
  )
  cp -a vim-${pkgver} gvim-${pkgver}
}

build() {
  msg2 "Building vim..."
  (cd vim-${pkgver}
    ./configure \
      --prefix=/usr \
      --localstatedir=/var/lib/vim \
      --with-features=huge \
      --with-compiledby='Guillaume Wells' \
      --enable-gpm \
      --enable-acl \
      --with-x=yes \
      --disable-gui \
      --enable-multibyte \
      --enable-cscope \
      --enable-netbeans \
      --enable-perlinterp=dynamic \
      --enable-pythoninterp=dynamic \
      --enable-python3interp=dynamic \
      --enable-rubyinterp=dynamic \
      --enable-luainterp=dynamic \
      --enable-tclinterp=dynamic \
      --disable-canberra
    make
  )
}

check() {
  cd vim-${pkgver}
  #You can desactivate test if there is minors fails
  TERM=xterm make -j1 test￼

}

package_vim-runtime() {
  pkgdesc+=' (shared runtime)'
  optdepends=('sh: support for some tools and macros'
              'python: demoserver example tool'
              'gawk: mve tools upport')
  backup=('etc/vimrc')

  cd vim-${pkgver}

  make -j1 VIMRCLOC=/etc DESTDIR="${pkgdir}" install
  # man and bin files belong to 'vim'
  rm -r "${pkgdir}"/usr/share/man/ "${pkgdir}"/usr/bin/

  # Don't forget logtalk.dict
  install -Dm 644 runtime/ftplugin/logtalk.dict \
    "${pkgdir}"/usr/share/vim/vim${_versiondir}/ftplugin/logtalk.dict

  # rc files
  install -Dm 644 "${srcdir}"/vimrc "${pkgdir}"/etc/vimrc
  install -Dm 644 "${srcdir}"/archlinux.vim \
    "${pkgdir}"/usr/share/vim/vimfiles/archlinux.vim

  # rgb.txt file
  install -Dm 644 runtime/rgb.txt \
    "${pkgdir}"/usr/share/vim/vim${_versiondir}/rgb.txt

  # no desktop files and icons
  rm -r "${pkgdir}"/usr/share/{applications,icons}

  # license
  install -dm 755 "${pkgdir}"/usr/share/licenses/vim-runtime
  ln -s /usr/share/vim/vim${_versiondir}/doc/uganda.txt \
    "${pkgdir}"/usr/share/licenses/vim-runtime/license.txt

  # pacman hook for documentation helptags
  install -Dm 644 "${srcdir}"/vimdoc.hook "${pkgdir}"/usr/share/libalpm/hooks/vimdoc.hook
}

package_vim() {
  depends=("vim-runtime=${pkgver}-${pkgrel}" 'gpm' 'acl' 'glibc' 'libgcrypt' 'pcre'
           'zlib' 'libffi')
  optdepends=('python2: Python 2 language support'
              'python: Python 3 language support'
              'ruby: Ruby language support'
              'lua: Lua language support'
              'perl: Perl language support'
              'tcl: Tcl language support')
  conflicts=('gvim' 'vim-minimal' 'vim-python3')
  provides=('xxd' 'vim-minimal' 'vim-python3')
  replaces=('vim-python3' 'vim-minimal')

  cd vim-${pkgver}
  make -j1 VIMRCLOC=/etc DESTDIR="${pkgdir}" install

  # provided by (n)vi in core
  rm "${pkgdir}"/usr/bin/{ex,view}

  # delete some manpages
  find "${pkgdir}"/usr/share/man -type d -name 'man1' 2>/dev/null | \
    while read _mandir; do
    cd "${_mandir}"
    rm -f ex.1 view.1 # provided by (n)vi
    rm -f evim.1    # this does not make sense if we have no GUI
  done

  # Runtime provided by runtime package
  rm -r "${pkgdir}"/usr/share/vim

  # remove gvim.desktop as not included
  rm "${pkgdir}"/usr/share/applications/gvim.desktop

  # license
  install -Dm 644 runtime/doc/uganda.txt \
    "${pkgdir}"/usr/share/licenses/${pkgname}/license.txt
}

# vim: ts=2 sw=2 et:

```

```shell
pacman -U vim-8.1.2268-2-x86_64.pkg.tar.xz vim-runtime-8.1.2268-2-x86_64.pkg.tar.xz
```

- Apply this patch for lusty explorer :
[patch](https://github.com/vim-scripts/LustyExplorer/pull/1/commits/0fb46f6e2e0bcd44094c7d2d959afe156348adcd)