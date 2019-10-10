# Maintainer: Sven-Hendrik Haase <sh@lutzhaase.com>
# Co-Maintainer: Konstantin Gizdov <arch@kge.pw>
# Contributor: Frederik Schwan <frederik dot schwan at linux dot com>
# Contributor: Simon Legner <Simon.Legner@gmail.com>

pkgname=bazel
pkgver=1.0.0
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
sha512sums=('3e51dfdf5883af3920149c74d0374524cb93b4d85fcaf402f3f7fae0e8e0a458be004365bfa7a0fc583a4f95e068ecaa2a53531ba315abb3e9180a7503db127f'
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
