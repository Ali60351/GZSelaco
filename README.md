# Selaco on macOS

This fork builds Selaco’s GZSelaco engine as an unofficial native macOS app. The Universal 2 app includes binaries for Apple silicon and Intel Macs. You need your own copy of Selaco on Steam to obtain the game data.

## Download

Download **`Selaco-universal.zip`** from the **Assets** section of the newest build. Each successful macOS build on `master` publishes a release tied to its source commit. [Releases](https://github.com/Ali60351/GZSelaco/releases)

To see build logs or download a recent build artifact, open the corresponding workflow run. [GitHub Actions](https://github.com/Ali60351/GZSelaco/actions/workflows/macos-compatibility.yml)

## macOS installation

1. Unzip `Selaco-universal.zip` and move `Selaco.app` to **Applications**.
2. Get `Selaco.ipk3` from your Steam copy. For this build, use the final **Chapter 1** archive. If you already installed the `chapter1` branch on Windows or Linux, copy the file from that installation. To fetch just the data on your Mac, open `steam://open/console` while signed in to Steam and run the following in the Steam console. [Chapter 1 depot metadata](https://steamdb.info/app/1592280/depots/?branch=chapter1)

   ```text
   download_depot 1592280 1592286 4748164188059173032
   ```

3. Copy `Selaco.ipk3` from the download path Steam prints into `~/Library/Application Support/Selaco-EA/`. Create the folder if needed. In Finder, use **Go → Go to Folder** to open it.
4. Open `Selaco.app`. The app uses ad hoc signing. If Gatekeeper blocks the download, verify that it came from this fork’s Releases page and follow Apple’s app approval steps. [Open a downloaded app on macOS](https://support.apple.com/en-us/102445)

To update, replace `Selaco.app` with the app from the new ZIP. The game data and saves live outside the app bundle.

### Bring over a Steam save

Download the `.zds` file for the game version you’re running and copy it into `~/Documents/Selaco-EA/Savegames/`. Open **Load Game** in Selaco to find it. Back up any existing save before replacing a file of the same name. [Selaco Steam Cloud files](https://store.steampowered.com/account/remotestorageapp/?appid=1592280)

## Testing status

- **Build and packaging.** GitHub Actions builds on Intel macOS 15 and verifies both the `arm64` and `x86_64` slices and the app signature. Minimum macOS version and full gameplay coverage across both architectures still need testing. [Successful Universal 2 build](https://github.com/Ali60351/GZSelaco/actions/runs/45452399854)
- **Chapter 1.** The final Chapter 1 Steam archive reached the end of startup in a local diagnostic, and a macOS build has had a user smoke test. Full campaign testing is still open.
- **Chapter 2.** This engine includes the upstream Chapter 2 update with ZScript `4.15.1`. Startup and gameplay with the original Chapter 2 archive on macOS still need testing. [Upstream Chapter 2 merge](https://github.com/TheCockatrice/GZSelaco/commit/8fab30043bb7bfe78034f21216520125f42b2228)

If you have multiple `.ipk3` files or need a startup log, run the app from Terminal with the archive you want to test.

```sh
/Applications/Selaco.app/Contents/MacOS/Selaco -stdout \
  -iwad "$HOME/Library/Application Support/Selaco-EA/Selaco.ipk3"
```

When reporting a problem, include the release tag, macOS version, chip, Steam game-data version, and the first error from the log.

## Building from source

See the [macOS build notes](README.osx.md) and the [build workflow](.github/workflows/macos-compatibility.yml) for the current MacPorts dependencies and CMake options.

## AI disclosure

OpenAI Codex assisted with compatibility analysis and patches, build automation, synthetic tests, and documentation for this fork. Maintainer review and tests on a Mac inform the compatibility status above.

## Credits and licensing

- **Altered Orbit Studios** created Selaco. **TheCockatrice** and the GZSelaco contributors develop the game’s engine fork. [Selaco on Steam](https://store.steampowered.com/app/1592280/Selaco/) · [GZSelaco engine source](https://github.com/TheCockatrice/GZSelaco)
- **CrowEater** created the macOS port this fork builds on. **Ali60351** maintains this fork and contributed compatibility work and testing. [CrowEater’s port](https://github.com/CrowEater/GZSelaco) · [Fork contributors](https://github.com/Ali60351/GZSelaco/graphs/contributors)

Copyright (c) 1998-2023 ZDoom + GZDoom teams, and contributors. [GZDoom](https://github.com/ZDoom/gzdoom)

Doom Source (c) 1997 id Software, Raven Software, and contributors.

The upstream GZDoom README thanks Coraline of the EDGE team for permission to use her README as a template. [EDGE](https://github.com/3dfxdev/EDGE)

The engine source is licensed under the [GNU GPL v3](LICENSE). See the [individual license files](docs/licenses/) for bundled components. Selaco’s game data is distributed separately through Steam.

### Upstream resources

- [ZDoom website](https://zdoom.org/) · [Forums](https://forum.zdoom.org/) · [Wiki and Programmer’s Corner](https://zdoom.org/wiki/) · [Discord](https://dsc.gg/zdoom)
- [GZDoom translation sheet](https://docs.google.com/spreadsheets/d/1pvwXEgytkor9SClCiDn4j5AH7FedyXS-ocCbsuQIXDU/edit?usp=sharing)
