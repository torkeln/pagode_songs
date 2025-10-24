# ChordPro Songbook Build System

This Meson-based build system automatically generates ChordPro PDFs for multiple instruments from `.cho` source files.

## Features

- **Multi-instrument support**: Guitar, Mandolin, and Cavaquinho (DGBD tuning)
- **Automatic dependency detection**: Only builds from existing `.cho` files
- **Professional chord diagrams**: Instrument-specific fingerings and tunings
- **PNG conversion**: Optional image generation from PDFs

## Supported Instruments

| Instrument | Tuning | Configuration |
|------------|--------|---------------|
| **Guitar** | EADGBE | Standard 6-string guitar |
| **Mandolin** | GDAE | 4-string mandolin |
| **Cavaquinho** | DGBD | Brazilian cavaquinho tuning |

## Quick Start

### 1. Prerequisites

```bash
# Required
sudo apt install meson ninja-build perl

# Optional (for PNG generation)
sudo apt install poppler-utils
```

### 2. Build Setup

```bash
# Setup build directory
meson setup builddir

# Build all PDFs
meson compile -C builddir
```

### 3. Build Results

Generated PDFs will be in the `builddir/` directory:

- `song_book_pagode_standard.pdf` - Standard formatting
- `song_book_pagode_guitar.pdf` - Guitar chord diagrams
- `song_book_pagode_mandolin.pdf` - Mandolin chord diagrams
- `song_book_pagode_cavaquinho.pdf` - Cavaquinho chord diagrams

## Advanced Usage

### Build Specific Targets

```bash
# Build only guitar version
meson compile -C builddir song_book_pagode_guitar

# Build only mandolin version
meson compile -C builddir song_book_pagode_mandolin

# Build only cavaquinho version
meson compile -C builddir song_book_pagode_cavaquinho
```

### Clean Build

```bash
# Remove build directory
rm -rf builddir

# Rebuild from scratch
meson setup builddir
meson compile -C builddir
```

## Files Structure

```
.
├── meson.build                    # Build configuration
├── song_book_pagode.cho           # Source ChordPro file
├── cavaquinho_dgbd.json          # Custom cavaquinho config
├── generate_png.sh               # PNG conversion script
├── builddir/                     # Generated PDFs
└── chordpro/                     # ChordPro source code
```

## Adding New Songs

1. Create a new `.cho` file in the root directory
2. Update `meson.build` to include the new file:

```meson
if fs.exists('your_new_song.cho')
  chordpro_files += 'your_new_song.cho'
  message('Found: your_new_song.cho')
endif
```

3. Rebuild:

```bash
meson compile -C builddir
```

## Customization

### Chord Diagrams

- **Guitar**: Uses standard ChordPro guitar configuration
- **Mandolin**: Uses ChordPro mandolin-ly configuration
- **Cavaquinho**: Uses custom DGBD tuning configuration

### Output Formats

The build system currently supports:
- PDF (primary format)
- PNG (via optional conversion script)

## Troubleshooting

### Common Issues

**"No ChordPro files found"**
- Ensure `.cho` files exist in the root directory
- Check that filenames match those in `meson.build`

**"perl not found"**
- Install Perl: `sudo apt install perl`

**"pdftoppm not found"**
- Install poppler-utils: `sudo apt install poppler-utils`

### Build Logs

Check build logs for detailed error information:
```bash
cat builddir/meson-logs/meson-log.txt
```

## License

This build system is provided as-is for generating ChordPro songbooks.
ChordPro software is subject to its own licensing terms.