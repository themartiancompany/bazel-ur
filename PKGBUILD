# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Robert Kirkman
# Maintainer: Chongyun Lee
# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Konstantin Gizdov <arch@kge.pw>
# Contributor: Frederik Schwan <frederik dot schwan at linux dot com>
# Contributor: Simon Legner <Simon.Legner@gmail.com>

_os="$( \
  uname \
    -o)"
_py="python"
_java_ver="21"
if [[ "${_os}" == "Android" ]]; then
  # I've set the java package as
  # termux calls it but in a full
  # Ur setup the Arch Linux and
  # Termux names would be the same.
  _java="opendjk-${_java_ver}"
  _majver="7"
  _minver="5.0"
  _pkgver="${_majver}.${_minver}"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _java="java-environment=${_java_ver}"
  _pkgver="8.1.0"
fi
_pkg=bazel
pkgname="${_pkg}"
pkgver="${_pkgver}"
pkgrel=1
_pkgdesc=(
  'Correct, reproducible,'
  'and fast builds for everyone'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  # The termux builds script
  # blacklists 32-bit architectures,
  # no idea why. Since it's them
  # who have requested me to write it,
  # I'll do as they do.
  # 'arm'
  # 'armv7l'
  'aarch64'
  # 'i686'
  'mips'
  'pentium4'
  'powerpc'
  'x86_64'
)
license=(
  'Apache-2.0'
)
url="https://${_pkg}.build"
depends=(
  "${_java}"
  'libarchive'
  'zip'
  'unzip'
  # Arch reports 'which' as a dependency,
  # not a makedepends as in the termux
  # build script.
  'which'
)
makedepends=(
  # The build recipe doesn't seem
  # to use 'git' so maybe it's the
  # invoked compile.sh script in the
  # build function.
  'git'
  'protobuf'
  "${_py}"
)
provides=(
  "${_pkg}${_majver}=${pkgver}"
)
conflicts=()
if [[ "${_os}" == "Android" ]]; then
  makedepends+=(
    # I suppose this could become
    # a depends if using the shared
    # library version of 'libandroid-spawn'
    "libandroid-spawn-static"
  )
  conflicts+=(
    "openjdk-11"
    "openjdk-17"
  )
fi
options=(
  '!debug'
  '!strip'
)
_http="https://github.com"
_ns="${_pkg}"
_url="${_http}/${_ns}/${_pkg}"
_tarname="${_pkg}-${pkgver}"
_patches=(
  "0001-strerror_r.patch"
  "0002-impl-wait3.patch"
  "0003-disable-sandbox.patch"
  "0004-spawn.patch"
  "0005-import-termux-patches.patch"
  "0006-force-use-external-patch_tools.patch"
  "0007-disable-module_maps.patch"
  "0008-run-elf-cleaner-for-bazel-tools.patch"
  "0009-bazelrc-path.patch"
)
_dep_patches=(
  "1001-BUILD"
  "1003-grpc.patch"
  "1005-upb-config.patch"
  "1002-cares-config.patch"
  "1004-protobuf.patch"
)
_patches_sums=(
  '5b0609d2080f47eb766b6bfef2ffa6c44e871e8701ca046c2228cfcfc2bab3ca9957f5ac0a9d492c128bdb2ecd8d4e4a296a4e5a54120b6c4f95c1c47b38e1e4'
  'd858bf4085e5f38abe8462796da41c86eb1f43b01aa875c41ee19ee3fad18f159f1eb26ba91755057a89a2213a43688c5e4b822121654d3508c409e703828cde'
  'fb3b4f6d1697c6a876fa0bee93533540203b146f6df3cda59ef7fe17001d07df88cf3eeac762888b09f58576e7e7a0e878666827ac4783ca68e11ec656c47e7d'
  '60447f576ff07744adb502b73f84df3d07279e5d478385cca66ee93fd2818edfdda87255e23a4777d07ca05cd7d3b700f39480432abe2304eb08c1e5df9c064c'
  '63e222f73e7c5c63c6cd8bb0f0a8bfb342d15b066ab30485f072893d75d9528e0d260470de25dd1adb9d92621e00ca4ff8e22124ccde5ef9ab63cffad2d3cf37'
  '40f12d77e5a1a18d90cb860537528b639065ed94713effb1adc7bdefb7d9d5b9b2dd0e946dadb5f45ec76b2c77561b6b4e6abd5846be4eb59f2ad0e9e139e555'
  '6dc86e1905c940d1f71e3e7c1098c984170379398a2d88eeea92e7423488b1b2d534038fe3b43a353abfb3f3d85968c853271fdfbe2b36aaea29cea96144f8a0'
  '876024236d64af4aa296da2147d4ccb9025d02c2ec5c28107c2e2382c8180c9301c9f29b2152f36d4083b5dac43cf236d86e77da0788d2b038f6f5779a95af08'
  'b2b1a605a190421461da1164a384dca1815e7681e7731f9f3d05bf553c9c8661a69308a848211a8805832290ce0871e0120c9233a32f086b56ba4b35f640bf49'
)
_dep_patches_sums=(
  '3a14a927999f997479a439d1809874dbf232e03ada8ca650cf1115ba61a78138461de7b55defbf4f64528f9ef8ff3c752de98f2d7b3b0df0f71f1a0706805cda'
  '62b0839c2653b95fb8a1ef51bc01dd93e0c451f7d1e899e988fbdfa56e361715a76cff803878fa7259608d3f3f9565a16645988162aa63a384eabab44ad3d437'
  '62e022687121a49317f0b93e1371afa69afad0d4eeb3439ec783da7eac4b453caad64aa32fd79f47bd3660d5bacf8b36ce188b53288bab21997f777d60ac93df'
  '9b06fb50bd574c081008ebf40376051c56b1b307339cd212ea115d1cabd02e9d646f7c38d6e7b8fd78634182bea1a62f5184ca5a3fcecf3ced607ad53bf38b62'
  '138c2a07d240b3f8261aff26032b11c16cfd396d24020aa29a3f7fb31bb9c3e0ff90ada80ab847a3d3989e456ccfbc6e09c5453417191595e8558f5d325c7937'
)
source=(
  "${_http}/releases/download/${pkgver}/${_tarname}-dist.zip"{,.sig}
)
b2sums=(
  '76da69aa2ee53db5c2151d02cfc165489207883245b3e5b16a44020babac8eb8441beceef47f970e27b9897a1add3f4954e3ca5d3b2bed18b8493fe9ab036775'
  'SKIP'
)
if [[ "${_os}" == "Android" ]]; then
  source+=(
    "${_patches[@]}"
    "${_dep_patches[@]}"
  )
  b2sums+=(
    "${_patches_sums[@]}"
    "${_dep_patches_sums[@]}"
  )
fi
validpgpkeys=(
  '71A1D0EFCFEB6281FD0437C93D5919B448457EE0'
)

_sed_verbose() {
	local \
    _path="${1}" \
    _expressions=()
  shift
  _expressions=(
    "$@"
  )
	sed \
    --follow-symlinks \
    -i".bak-nix" \
    "${_expressions[@]}" \
    "${_path}"
	diff \
    -U0 \
    "${_path}.bak-nix" \
    "${_path}" | \
    sed \
      "s/^/  /" \ || \
    true
	rm \
    -f \
    "${_path}.bak-nix"
}

_fix_hardcoded_paths() {
	local \
    _builtins_bzl \
    _devtools_dir \
    _devtools_build_dir \
    _nix_ns \
    _nix_ver \
    _nixpkgs_url \
    _nixpkgs_target_url \
    _nixpkgs_category \
    _nixpkgs_path \
    _nixpkgs_ref \
    _path \
    _file \
    _msg=()
  _nix_ns="NixOS"
  _nix_ver="release-23.11"
  _nixpkgs_url="${_http}/${_nix_ns}/nixpkgs"
  _nixpkgs_target_url="${_nixpkgs_url}/blob/${_nix_ver}/pkgs"
  _nixpkgs_category="development/tools/build-managers"
  _nixpkgs_path="${_nixpkgs_category}/${_pkg}/${_pkg}_${_majver}"
  _nixpkgs_ref="${_nixpkgs_path}/default.nix"
  _msg=(
    "Fixing hard-coded paths."
    "Reference:"
      "'${_nixpkgs_ref}'"
  )
  echo \
    "${_msg[*]}"
  _msg
	# Unzip builtins_bzl.zip so the contents get patched
  _devtools_dir="src/main/java/com/google/devtools"
  _devtools_build_dir="${_devtools_dir}/build"
  _builtins_bzl="${_devtools_build_dir}/lib/${_pkg}/rules/builtins_bzl"
	unzip \
    "${_builtins_bzl}.zip" \
    -d \
      "${_builtins_bzl}_zip" >/dev/null
	rm \
    "${_builtins_bzl}.zip"
	builtins_bzl="${_builtins_bzl}_zip/builtins_bzl"
	echo
  _msg=(
    "Substituting */bin/* hardcoded paths in"
    "in '${_devtools_dir}'."
  )
	echo \
    "${_msg[*]}"
	# Prefilter the files with grep for speed
	grep \
    -rlZ \
    "/bin/" \
    "${_devtools_dir}" \
		"src/main/starlark/builtins_bzl/common/${_py}" \
		"tools" | \
    while IFS="" \
          read \
            -r \
            -d "" _path; do
		  # If you add more replacements here, you must change the grep above!
		  # Only files containing /bin are taken into account.
		  _sed_verbose \
        "${_path}" \
        -e "s!/usr/local/bin/bash!${TERMUX_PREFIX}/bin/bash!g" \
        -e "s!/usr/bin/bash!${TERMUX_PREFIX}/bin/bash!g" \
        -e "s!/bin/bash!${TERMUX_PREFIX}/bin/bash!g" \
        -e "s!/usr/bin/env bash!${TERMUX_PREFIX}/bin/bash!g" \
        -e "s!/usr/bin/env python2!${TERMUX_PREFIX}/bin/python!g" \
        -e "s!/usr/bin/env python!${TERMUX_PREFIX}/bin/python!g" \
        -e "s!/usr/bin/env!${TERMUX_PREFIX}/bin/env!g" \
        -e "s!/bin/true!${TERMUX_PREFIX}/bin/true!g"
	  done
	# Fixup scripts that generate scripts.
  # Not fixed up by patchShebangs below.
	_sed_verbose \
    "scripts/bootstrap/compile.sh" \
		-e "s!/bin/bash!${TERMUX_PREFIX}/bin/bash!g"
	# reconstruct the now patched builtins_bzl.zip
	pushd \
    "${_builtins_bzl}_zip" &>/dev/null
	zip \
    "../builtins_bzl.zip" \
    $(find \
        "builtins_bzl" \
        -type \
          "f") >/dev/null
	rm \
    -rf \
    "builtins_bzl"
	popd \
    &>/dev/null
	rmdir \
    "${_builtins_bzl}_zip"
	# Fix shebangs
	while \
    IFS= read \
           -r \
           -d '' _file; do
		if head \
         -c \
           100 \
         "${_file}" | \
         head \
           -n \
             1 | \
           grep \
             -E \
               "^#!.*/bin/.*" | \
             grep \
               -q \
               -E \
               -v \
               "^#! ?${TERMUX_PREFIX}"; then
			_sed_verbose \
        "${_file}" \
        -E "1 s@^#\!(.*)/bin/(.*)@#\!${TERMUX_PREFIX}/bin/\2@"
		fi
	done < \
    <(find \
        -L \
        "." \
        -type \
          "f" \
        -print0)
}

prepare() {
  local \
    _patch
  if [[ "${_os}" == "Android" ]]; then
    # The sources seems to be in
    # the archive's root so they
    # will be in the srcdir
    # directly
    for _patch in "${_patches[@]}"; do
      patch \
        -uNp1 \
        -i \
          "${srcdir}/${_patch}" || \
        return \
          1
    done
    _fix_hardcoded_paths
    mkdir \
      -p \
      "third_party/termux-patches"
    for _patch in "${_dep_patches[@]}"; do
      cp \
        -Rfv \
        "${_patch}" \
	"third_party/termux-patches/${_patch#100*-}"
    done
  fi
}

_usr_get() {
  local \
    _bin
  _bin="$( \
    dirname \
      "$(command \
           -v \
           "env")")"
  echo \
    "$(dirname \
         "${_bin}")"
}

build() {
  local \
    _extra_bazel_args=() \
    _lib
  _extra_bazel_args+=(
    --tool_java_runtime_version="local_jdk"
  )
  if [[ "${_os}" == "Android" ]]; then
    _extra_bazel_args+=(
      # --keep_going
      --verbose_failures
      --action_env="ANDROID_DATA"
      --action_env="ANDROID_ROOT"
      --action_env="LD_PRELOAD"
    )
    _lib="$( \
      _usr_get)/lib)"
    export \
      JAVA_HOME="${_lib}/jvm/java-${_java_ver}-openjdk"
  fi
  EMBED_LABEL="${pkgver}" \
  EXTRA_BAZEL_ARGS="${_extra_bazel_args[*]}" \
  VERBOSE=1 \
  "./compile.sh"
  "./output/bazel" \
    build \
      "scripts:bazel-complete.bash"
  cd \
    "output"
  "./bazel" \
    shutdown
}

package() {
  local \
    _dir
  install \
    -Dm755 \
      "${srcdir}/scripts/packages/${_pkg}.sh" \
      "${pkgdir}/usr/bin/${_pkg}"
  install \
    -Dm755 \
    "${srcdir}/output/${_pkg}" \
    "${pkgdir}/usr/bin/${_pkg}-real"
  install \
    -Dm644 \
    "${srcdir}/${_pkg}-bin/scripts/${_pkg}-complete.bash" \
    "${pkgdir}/usr/share/bash-completion/completions/${_pkg}"
  install \
    -Dm644 \
    "${srcdir}/scripts/zsh_completion/_${_pkg}" \
    "${pkgdir}/usr/share/zsh/site-functions/_${_pkg}"
  mkdir \
    -p \
    "${pkgdir}/usr/share/${_pkg}"
  for _dir \
    in "third_party" "tools"; do
    cp \
      -r \
      "${srcdir}/${_dir}" \
      "${pkgdir}/usr/share/${_pkg}/"
  done
}

# vim:set ts=2 sw=2 et:



