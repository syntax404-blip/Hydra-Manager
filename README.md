<img width="1000" height="512" alt="Hydra Manager" src="https://github.com/user-attachments/assets/8c86a54b-8013-4dd7-a4e1-d6c39bef3ff5" />

# Hydra Manager

Hydra Manager is a customizable download manager for macOS, built with Rust. It supports segmented HTTP and HTTPS transfers, priority queues, per-download speed limits, and a multilingual interface. The app is distributed as a universal binary for Intel and Apple Silicon Macs.

## Features

- Download files over HTTP and HTTPS.
- Split supported downloads into 1–16 segments.
- Fall back to a single connection when the server does not support byte ranges.
- Set each download's priority to low, normal, or high.
- Limit the speed of individual downloads or leave it unlimited.
- Run 1–6 downloads at the same time.
- Pause, resume, cancel, and retry downloads.
- Choose a filename and destination folder for each download.
- Set a default download folder and default transfer options.
- Prevent accidental overwrites by choosing a unique filename.
- Search downloads by filename and filter the queue and transfer history.
- See progress, transferred data, per-download speed, and total speed.
- Copy a download's URL or reveal its file in Finder.
- Restore preferences, queue, and download history after restarting the app.
- Personalize the interface with dark, light, and monochrome themes, four accent colors, compact mode, scaling, and animation controls.
- Use the interface in English, Spanish, German, French, Catalan, or Russian.
- Paste a URL with `⌘V` when adding a download.

## Install

Download the latest `HydraManager-macOS.zip` archive from [GitHub Releases](../../releases/latest), unzip it, and move `Hydra Manager.app` to your Applications folder.

Release builds are currently ad-hoc signed and are not notarized with an Apple Developer ID. If macOS blocks the app, control-click it in Finder, choose **Open**, and confirm the prompt.

## Build from source

Requirements:

- macOS 12 or later
- Rust and Cargo installed through [rustup](https://rustup.rs/)
- Xcode Command Line Tools
- The `aarch64-apple-darwin` and `x86_64-apple-darwin` Rust targets

Install the targets and build the universal app:

```sh
rustup target add aarch64-apple-darwin x86_64-apple-darwin
./scripts/build_macos.sh
open "outputs/Hydra Manager.app"
```

The first build downloads dependencies from crates.io. To choose a different output directory, set `HYDRA_OUTPUT_DIR` when running the build script:

```sh
HYDRA_OUTPUT_DIR="$PWD/dist" ./scripts/build_macos.sh
```

To run the app in development mode:

```sh
cargo run
```

## Known limitations

- If the app closes during an active transfer, that download is restored to the queue and starts again from the beginning. Partial file data is not currently saved for byte-by-byte resume.
- Segmented downloads require the server to support HTTP byte ranges. Hydra Manager falls back to a single connection when segmentation is unavailable.
- Downloads that require custom headers, cookies, or authentication are not supported yet.

## License

Hydra Manager is declared as MIT licensed in `Cargo.toml`.
