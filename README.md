# Lean IPTV: libmpv source

Lean IPTV uses libmpv and FFmpeg under the GNU Lesser General Public License,
version 3 or later, as a separate library (`libmpv.so`).

The release of this repository holds the complete corresponding source of that
library: the build repository
[Predidit/libmpv-android-video-build](https://github.com/Predidit/libmpv-android-video-build)
at commit `dd2bfba820`, with its `default` flavor configuration, its patches, and
the populated `buildscripts/deps` directory after `download-deps.sh` and
`patch.sh` have run. Git metadata is left out. shaderc, glslang, SPIRV-Tools and
libc++ are as shipped in Android NDK 27.2.12479018.

Notices: https://dataprospectors.at/en/lean-iptv/open-source
