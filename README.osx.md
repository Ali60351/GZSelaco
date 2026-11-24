# macOS build notes

For downloads, setup, and game-data compatibility, see the [macOS installation guide](README.md#macos-installation).

## Building from source

Install Xcode command-line tools, CMake, Python 3, and MacPorts for your macOS version. The workflow installs the following MacPorts dependencies with `+universal` for the Universal 2 build. [Current CI recipe](.github/workflows/macos-compatibility.yml)

```sh
sudo /opt/local/bin/port -N sync
sudo /opt/local/bin/port -N install \
  glib2 +universal libsdl2 +universal libsndfile +universal \
  libvpx +universal MoltenVK +universal openal-soft +universal
```

Use the CMake options in the workflow’s **Build Selaco.app** step. It builds the SDL backend for `arm64;x86_64` and uses the ZMusic libraries under `bin/osx/zmusic`. The packaging script copies the dependencies into `Selaco.app` and adjusts their library paths. The workflow checks both architectures, signs the app ad hoc, and zips it. [Packaging script](tools/scripts/package_selaco_osx.py)

## OpenGL on older Intel Macs

CrowEater’s original port notes report that OpenGL on a 2019 Intel iMac could show a black menu background because the driver lacked BC7 texture support. Vulkan rendered those textures on the same Mac. If you see the same symptom, try the Vulkan renderer. [Original macOS port notes](https://github.com/CrowEater/GZSelaco/blob/f19eea1/README.osx.md)

The original port also provided a texture conversion script for OpenGL. It generates a patch WAD and updates the engine configuration. [Texture conversion script](tools/scripts/build_dxt_wad.py)
