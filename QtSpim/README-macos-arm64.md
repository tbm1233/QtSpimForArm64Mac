# Building QtSpim for Apple Silicon

QtSpim can be built as a native arm64 macOS application from this source tree. The build uses the existing Qt 5 front end and the shared SPIM simulator sources.

## Requirements

- An Apple Silicon Mac with Xcode Command Line Tools
- Qt 5.15 for macOS, including `qmake` and `macdeployqt`
- `bison` and `flex` (available with the Xcode Command Line Tools)

Install Qt 5.15 with a package manager or the Qt installer. If `qmake` is not on `PATH`, provide its path with `QMAKE`, for example:

```sh
QMAKE=/path/to/Qt/5.15.2/macos/bin/qmake ../bin/build-qtspim-macos-arm64
```

Otherwise run the build script from the project root:

```sh
./bin/build-qtspim-macos-arm64
```

The script checks that it is running on arm64 and using Qt 5, builds the QtSpim app, bundles its Qt frameworks and required plugins, removes any unused Qt Virtual Keyboard framework/plugin/QML module, applies a local ad-hoc signature, and places the finished app at `build-qtspim-macos-arm64/QtSpimForArm64Mac.app`. QtSpim does not use the Virtual Keyboard component; the build also verifies that the executable does not link it and that no matching component files remain in the bundle. Open the app in Finder or copy it to Applications. The local signature allows macOS to validate the finished bundle, but it is not a Developer ID signature or notarization for public distribution.

QtSpim's existing macOS project settings and `macinfo.plist` are used. Qt 6 is not supported by this legacy source without a separate port because the interface still uses Qt 5 APIs.
