project('adwaita-icon-theme', version : '51.0', meson_version : '>= 0.64.0')

pkg = import('pkgconfig')
pkg.generate(
  name : 'adwaita-icon-theme',
  description : 'A collection of icons used as the basis for GNOME themes',
  dataonly : true,
)

licenses_dir = get_option('datadir') / 'licenses' / 'adwaita-icon-theme'
install_data('COPYING', install_dir : licenses_dir, install_tag : 'runtime')
install_data('COPYING_CCBYSA3', install_dir : licenses_dir, install_tag : 'runtime')
install_data('COPYING_LGPL', install_dir : licenses_dir, install_tag : 'runtime')

adwaita_dir = get_option('datadir') / 'icons' / 'Adwaita'
install_data('index.theme', install_dir : adwaita_dir, install_tag : 'runtime')

install_subdir(
  'Adwaita',
  install_dir: adwaita_dir,
  strip_directory : true,
  install_tag : 'runtime',
)

files('Adwaita/scalable/places/folder.svg')
if host_machine.system() == 'windows'
  install_data(
    'Adwaita/scalable/places/folder.svg',
    install_dir: adwaita_dir / 'scalable' / 'status',
    rename: 'folder-open.svg',
    install_tag : 'runtime',
  )
else
  install_symlink(
    'folder-open.svg',
    install_dir: adwaita_dir / 'scalable' / 'status',
    install_tag: 'runtime',
    pointing_to: '../places/folder.svg',
  )
endif

gtk_update_icon_cache = find_program(
  'gtk4-update-icon-cache',
  'gtk-update-icon-cache',
  required : true,
)
meson.add_install_script(
  gtk_update_icon_cache,
  '-qtf',
  get_option('prefix') / adwaita_dir,
  skip_if_destdir: true,
)
