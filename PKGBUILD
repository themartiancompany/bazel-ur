# Maintainer: Sven-Hendrik Haase <svenstaro@gmail.com>
# Maintainer: Konstantin Gizdov <arch@kge.pw>
# Contributor: Frederik Schwan <frederik dot schwan at linux dot com>
# Contributor: Simon Legner <Simon.Legner@gmail.com>

pkgname=bazel
pkgver=1.2.0
pkgrel=1
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch=('x86_64')
license=('Apache')
url='https://bazel.io/'
depends=('java-environment=11' 'libarchive' 'zip' 'unzip')
makedepends=('git' 'protobuf' 'python')
options=('!distcc' '!strip')
source=("https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip"
        "https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"
        'grpc_rename_gettid.patch')
sha512sums=('eaa3e27d0ddd6102fea4fcdf5f4379355954ba25cd2f4b3530071d077411f8a501041d8fda9ac90325244296f31072faaebd91cf6338893752b25212822a6be9'
            'SKIP'
            '0d4dc5c5931ff3a16bb9ac228ec560fc0115444a3d3787f12866e11e8b3833ee8a26cc65c97aa9898c1f7a6c380820d62544d2ed7bed0d6f21aa4293e244eb04')
validpgpkeys=('71A1D0EFCFEB6281FD0437C93D5919B448457EE0')

prepare() {
  # fix gRPC: https://github.com/grpc/grpc/pull/18950
  patch -Np0 -i "${srcdir}/grpc_rename_gettid.patch" -d third_party/grpc
}

build() {
  env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" ./compile.sh
  ./output/bazel build scripts:bazel-complete.bash
  cd output
  ./bazel shutdown
}

package() {
  install -Dm755 "${srcdir}/scripts/packages/bazel.sh" "${pkgdir}/usr/bin/bazel"
  install -Dm755 "${srcdir}/output/bazel" "${pkgdir}/usr/bin/bazel-real"
  install -Dm644 "${srcdir}/bazel-bin/scripts/bazel-complete.bash" "${pkgdir}/usr/share/bash-completion/completions/bazel"
  install -Dm644 "${srcdir}/scripts/zsh_completion/_bazel" "${pkgdir}/usr/share/zsh/site-functions/_bazel"
  mkdir -p "${pkgdir}/opt/bazel"
  for d in examples third_party tools; do
    cp -r "${srcdir}/${d}" "${pkgdir}/opt/bazel/"
  done
}
# vim:set ts=2 sw=2 et:
