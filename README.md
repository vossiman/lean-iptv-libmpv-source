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

## Replacing libmpv.so in the app

1. Build `libmpv.so` from this source, keeping the libmpv client API.
2. Copy the app off the device: `adb shell pm path at.dataprospectors.leaniptv`
   lists its APKs. Pull each with `adb pull`.
3. In the APK that holds `lib/<abi>/libmpv.so`, remove the old library and
   signature with `zip -d app.apk lib/<abi>/libmpv.so 'META-INF/*'`, then add
   the new library uncompressed with `zip -0`.
4. For every APK of the app, run `zipalign -P 16 -f 4 in.apk out.apk`, then
   `apksigner sign --ks own.jks out.apk`, using one key of your own.
5. Uninstall the Play copy, because Android refuses an update signed with a
   different key. Then install with `adb install-multiple base.apk split_*.apk`,
   or `adb install` for a single APK.
