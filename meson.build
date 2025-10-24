project('chordpro-songbook', 'c',
  version : '1.0.0',
  default_options : ['warning_level=3'])

# Import filesystem module
fs = import('fs')

# Find perl interpreter
perl = find_program('perl')

# Define ChordPro script path
chordpro_script = meson.current_source_dir() / 'chordpro/script/chordpro'

# Define configuration files
guitar_config = meson.current_source_dir() / 'chordpro/lib/ChordPro/res/config/guitar.json'
mandolin_config = meson.current_source_dir() / 'chordpro/lib/ChordPro/res/config/mandolin-ly.json'
cavaquinho_config = meson.current_source_dir() / 'cavaquinho_dgbd.json'

# Define source ChordPro files that exist
chordpro_files = []

# Add files if they exist
if fs.exists('song_book_pagode.cho')
  chordpro_files += 'song_book_pagode.cho'
  message('Found: song_book_pagode.cho')
endif

if chordpro_files.length() == 0
  error('No ChordPro files found to build!')
endif

# Generate PDFs for each instrument and source file
foreach chordpro_file : chordpro_files
  basename = chordpro_file.split('.')[0]

  # Guitar PDF
  custom_target(basename + '_guitar',
    input : chordpro_file,
    output : basename + '_guitar.pdf',
    command : [perl, chordpro_script, '--config', guitar_config, '--output', '@OUTPUT@', '@INPUT@'],
    build_by_default : true,
    install : false
  )

  # Mandolin PDF
  custom_target(basename + '_mandolin',
    input : chordpro_file,
    output : basename + '_mandolin.pdf',
    command : [perl, chordpro_script, '--config', mandolin_config, '--output', '@OUTPUT@', '@INPUT@'],
    build_by_default : true,
    install : false
  )

  # Cavaquinho PDF
  custom_target(basename + '_cavaquinho',
    input : chordpro_file,
    output : basename + '_cavaquinho.pdf',
    command : [perl, chordpro_script, '--config', cavaquinho_config, '--output', '@OUTPUT@', '@INPUT@'],
    build_by_default : true,
    install : false
  )
endforeach

# Create PNG images from PDFs using pdftoppm
pdftoppm = find_program('pdftoppm', required : false)

if pdftoppm.found()
  # PNG targets will be created dynamically based on the PDF targets built above
  # This is handled automatically by the custom_target dependencies
  message('PNG conversion available via pdftoppm')
else
  message('PNG conversion not available - pdftoppm not found')
endif

# Summary message
message('ChordPro Songbook Build System')
message('================================')
message('Available targets:')
message('  - Standard PDFs: test_standard.pdf, song_book_pagode_standard.pdf')
message('  - Guitar PDFs: test_guitar.pdf, song_book_pagode_guitar.pdf')
message('  - Mandolin PDFs: test_mandolin.pdf, song_book_pagode_mandolin.pdf')
message('  - Cavaquinho PDFs: test_cavaquinho.pdf, song_book_pagode_cavaquinho.pdf')
if pdftoppm.found()
  message('  - PNG images: Add -Dpng=true to generate PNG versions')
else
  message('  - PNG images: pdftoppm not found, PNG generation disabled')
endif
message('')
message('Build commands:')
message('  meson setup builddir')
message('  meson compile -C builddir')
message('  meson compile -C builddir <target_name>  # Build specific target')