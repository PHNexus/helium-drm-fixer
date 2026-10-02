# Helium DRM Fixer

A CLI tool that fixes DRM issues in the Helium browser by copying WidevineCdm from Chrome (or other Chrome-based browsers).

> **Note:** This is a fork of [vikas5914/helium-drm-fixer](https://github.com/vikas5914/helium-drm-fixer). All credit goes to [@vikas5914](https://github.com/vikas5914). I do not own the original project.

> **Used by:** [PHNexus/Hyprland-configs](https://github.com/PHNexus/Hyprland-configs) — this tool is automatically run by the dotfiles `install.sh` to fix DRM for the Helium browser.

## Why Helium DRM?

Helium browser often has issues with DRM-protected content because it doesn't include WidevineCdm. This tool automatically copies WidevineCdm from your Chrome installation to Helium, enabling basic Widevine support for sites that accept it.

## Installation

```bash
bun install
```

## Usage

```bash
bun run cli.ts
```

Or after building:

```bash
bun run build
./dist/fix-helium-drm
```

## How It Works

1. **Finds Chrome WidevineCdm**: The tool searches for your Chrome (or other Chromium-based browser) installation and locates the WidevineCdm directory.
2. **Finds Helium installation**: Locates your Helium browser installation.
3. **Copies WidevineCdm**: Copies the WidevineCdm files from Chrome to Helium.
4. **Automatic download**: If Chrome is not found locally, the tool will download it from GitHub releases (Windows only).

## Limitations

This tool only makes Helium able to load Widevine. It does not change Helium's Chromium build, browser identity, codecs, HDCP support, Widevine certification, or Verified Media Path status.

That is why DRM can work on some sites, such as YouTube or Crunchyroll, but still fail on stricter services such as Netflix or Amazon Prime Video. Those services can require an approved browser, output protection, VMP, or other license-server checks that copying `WidevineCdm` cannot satisfy.

## Features

- Automatic Chrome/Helium detection
- Automatic Chrome download if not found (Windows only)
- Download caching with checksum verification
- Progress tracking for downloads
- Cross-platform support (Windows, macOS, Linux)
- Type-safe TypeScript implementation

## Custom paths

If this script fails to find your browser, you can specify the path to it manually:

```bash
sudo bun run cli.ts --chrome-path /usr/bin/google-chrome-stable --helium-path /usr/bin/helium-browser
```

You can find the path on your system by running `which google-chrome-stable` on macOS and Linux.

## Automatic install via Hyprland-configs

If you're using the [Hyprland-configs](https://github.com/PHNexus/Hyprland-configs) dotfiles, this tool is run automatically by the `install.sh` script:

- Temporarily installs Google Chrome via AUR
- Runs the DRM fix against the Helium installation
- Uninstalls Chrome and cleans up traces
- No manual steps needed

## Development

```bash
# Run tests
bun test

# Lint code
bun run lint

# Auto-fix lint issues
bun run lint:fix

# Type checking
bun run typecheck

# Build executable
bun run build
```

## Troubleshooting

### "Helium browser not found"
Ensure you have Helium browser installed. Download it from [https://helium.is/](https://helium.is/).

### "Chrome not found"
The tool will automatically download Chrome. If this fails, install Chrome manually from [https://www.google.com/chrome/](https://www.google.com/chrome/).

### "Failed to copy WidevineCdm"
Make sure you have write permissions to the Helium application directory.

## License

MIT — original license belongs to [@vikas5914](https://github.com/vikas5914).

## Credits

- [@vikas5914](https://github.com/vikas5914) — original author
- [Helium Browser](https://helium.is/) — the browser this tool fixes
- [Bun](https://bun.sh/) — fast JavaScript runtime
