# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Konstantin Gizdov <arch@kge.pw>
# Contributor: Frederik Schwan <frederik dot schwan at linux dot com>
# Contributor: Simon Legner <Simon.Legner@gmail.com>

pkgname=bazel
pkgver=7.3.2
pkgrel=1
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch=('x86_64')
license=('Apache-2.0')
url='https://bazel.build/'
depends=('java-environment=21' 'libarchive' 'zip' 'unzip' 'which')
makedepends=('git' 'protobuf' 'python')
options=('!debug' '!strip')
source=(
  "https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip"{,.sig}
  $pkgname-7.0.2-python_312.patch
)
b2sums=('d650255d9573a831bfc0a7a68f0cce71e606bdee6c0eac1e6582032663745c61ac83d3310f9ea60b88886f0fb48278bb75852bcc51b23060a739f932868b34cc'
        'SKIP'
        'e13a9c5b43336941d1bb35685d6bf8761b70349aca705ff6202018180e7291efcb4dbf8415ad9c788dcf6f5d956cbca8e1d8a8b663a504dd537e6f682ad04202')
validpgpkeys=('71A1D0EFCFEB6281FD0437C93D5919B448457EE0')

prepare() {
  # replace Python 3.12 incompatible code https://github.com/bazelbuild/bazel/issues/21537
  patch -Np1 -i $pkgname-7.0.2-python_312.patch
}

build() {
  EMBED_LABEL=$pkgver EXTRA_BAZEL_ARGS="--tool_java_runtime_version=local_jdk" ./compile.sh
  ./output/bazel build scripts:bazel-complete.bash
  cd output
  ./bazel shutdown
}

package() {
  install -Dm755 "${srcdir}/scripts/packages/bazel.sh" "${pkgdir}/usr/bin/bazel"
  install -Dm755 "${srcdir}/output/bazel" "${pkgdir}/usr/bin/bazel-real"
  install -Dm644 "${srcdir}/bazel-bin/scripts/bazel-complete.bash" "${pkgdir}/usr/share/bash-completion/completions/bazel"
  install -Dm644 "${srcdir}/scripts/zsh_completion/_bazel" "${pkgdir}/usr/share/zsh/site-functions/_bazel"
  mkdir -p "${pkgdir}/usr/share/bazel"
  for d in examples third_party tools; do
    cp -r "${srcdir}/${d}" "${pkgdir}/usr/share/bazel/"
  done
}
# vim:set ts=2 sw=2 et:
