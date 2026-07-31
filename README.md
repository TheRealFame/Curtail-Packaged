# Curtail Linux Repackaging

Repackages the official Curtail image compressor into **AppImage** and **Debian** formats with GitHub Actions CI/CD.

> This README was generated with AI assistance.

## Packages Built

| Format | Use Case |
|--------|----------|
| **AppImage** | Universal Linux (any distro with FUSE) |
| **Debian (.deb)** | Ubuntu, Debian, Mint, Pop!_OS |

## Quick Start

### Download Latest Release
Go to [Releases](https://github.com/TheRealFame/curtail-packaging/releases) and grab:
- `curtail-x86_64.AppImage` — run anywhere
- `curtail_*.deb` — install on Debian/Ubuntu

### Install

```bash
# AppImage (universal)
chmod +x curtail-x86_64.AppImage
./curtail-x86_64.AppImage

# Debian/Ubuntu
sudo dpkg -i curtail_*.deb
sudo apt-get install -f
```

## Required Dependencies (All Formats)

Curtail uses external CLI tools for compression — **not bundled** per Debian policy:

```bash
# Ubuntu/Debian/Mint
sudo apt install oxipng pngquant jpegoptim webp scour

# Fedora/RHEL
sudo dnf install oxipng pngquant jpegoptim libwebp scour

# Arch/Manjaro
sudo pacman -S oxipng pngquant jpegoptim libwebp scour

# openSUSE
sudo zypper install oxipng pngquant jpegoptim libwebp-tools scour
```

| Tool | Format | Purpose |
|------|--------|---------|
| `oxipng` | PNG | Lossless/lossy optimization |
| `pngquant` | PNG | Lossy quantization |
| `jpegoptim` | JPEG | Lossless/lossy optimization |
| `webp` (`cwebp`) | WebP | Encode WebP |
| `scour` | SVG | SVG optimization |

## Build Locally

```bash
git clone https://github.com/TheRealFame/curtail-packaging
cd curtail-packaging

# Build AppImage
./build-appimage.sh

# Build .deb (on Debian/Ubuntu)
cd curtail-src && debuild -us -uc -b
```

## GitHub Actions CI/CD

Workflow: [`.github/workflows/build.yml`](.github/workflows/build.yml)

Triggers:
- Push tags `v*` or `1.*` → builds + creates Release
- Pull requests → builds artifacts
- Manual dispatch

Outputs per release:
- `curtail-x86_64.AppImage`
- `curtail_*.deb`

## Upstream

- **Source**: https://github.com/Huluti/Curtail
- **License**: GPL-3.0-or-later
- **Flatpak**: https://flathub.org/apps/com.github.huluti.Curtail

## Troubleshooting

See [PACKAGING_TROUBLESHOOTING.md](PACKAGING_TROUBLESHOOTING.md) for:
- AppImage FUSE issues
- Missing compression tools
- Python module errors
- Desktop integration problems