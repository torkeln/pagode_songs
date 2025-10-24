# ChordPro Songbook - Pagode Songs

A collection of Brazilian pagode and Swedish songs formatted for ChordPro with support for multiple instruments.

## Instruments Supported

- **Guitar** - Standard EADGBE tuning
- **Mandolin** - GDAE tuning  
- **Cavaquinho** - Brazilian DGBD tuning

## Songs Included

1. **Canta Canta Minha Gente** - Traditional Brazilian
2. **Cheia de Manias** - Raça Negra
3. **Marinheiro Só** - Traditional
4. **Deidres Samba** - Cornelis Vreeswijk
5. **Somliga Går Med Trasiga Skor** - Cornelis Vreeswijk

## Building Locally

### Prerequisites
- Perl with ChordPro installed
- Meson build system
- Ninja build backend

### Install ChordPro
```bash
cpan App::Music::ChordPro
```

### Build PDFs
```bash
meson setup builddir
meson compile -C builddir
```

Generated PDFs will be in `builddir/`:
- `song_book_pagode_guitar.pdf`
- `song_book_pagode_mandolin.pdf`
- `song_book_pagode_cavaquinho.pdf`

### Generate PNG Images
```bash
./generate_png.sh
```

## GitHub Actions - Automated Building

This repository uses GitHub Actions for automated building:

### Automatic Builds
- **Triggers**: Push to main/master, pull requests, manual dispatch
- **Builds**: PDFs for all instruments
- **Artifacts**: Downloadable PDFs and PNG images (30-day retention)

### Creating Releases
```bash
# Tag and push for automatic release
git tag v1.0.0
git push origin v1.0.0
```

### Manual Builds
1. Go to **Actions** tab in GitHub
2. Select "Build ChordPro Songbook" 
3. Click "Run workflow"

## File Structure

```
.
├── song_book_pagode.cho          # Main songbook source
├── cavaquinho_dgbd.json          # Custom cavaquinho config
├── meson.build                   # Build system configuration
├── generate_png.sh               # PNG conversion utility
├── .github/workflows/            # GitHub Actions
│   ├── build-songbook.yml        # Automatic PDF building
│   └── release.yml               # Release creation
└── builddir/                     # Generated PDFs
    ├── song_book_pagode_guitar.pdf
    ├── song_book_pagode_mandolin.pdf
    └── song_book_pagode_cavaquinho.pdf
```

## ChordPro Format

Songs use standard ChordPro format with proper metadata:

```chordpro
{new_song}
{title: Song Title}
{artist: Artist Name}
{key: Am}

{start_of_verse}
[Am]Lyrics with [G]chords [C]above [Am]words
{end_of_verse}

{start_of_chorus}
[F]Chorus [C]lyrics [G]here [Am]
{end_of_chorus}
```

## Custom Cavaquinho Configuration

The Brazilian cavaquinho uses DGBD tuning (D4-G4-B4-D5) with custom chord fingerings optimized for this tuning. All common chords including minor 7th variations are supported.

## Contributing

1. Edit `.cho` files with proper ChordPro formatting
2. Test builds locally with `meson compile -C builddir`
3. Commit and push - GitHub Actions will build automatically
4. Create releases with git tags for distribution

## License

Song arrangements and chord progressions for educational use.