project('fatfs', 'c', version: 'v0.15.1', meson_version: '>=1.3.0', default_options: ['buildtype=release'])

common_cflags = [
    '-Wno-conversion',
    '-Wno-pedantic',
    '-Wno-sign-conversion',
    '-Wno-comment',
    '-Wno-switch-enum',
    '-Wno-unused-parameter',
]


# Create configuration data object
ffconfig = configuration_data()

# Function Configurations
ffconfig.set('FF_FS_READONLY', get_option('FATFS_FS_READONLY'))
ffconfig.set('FF_FS_MINIMIZE', get_option('FATFS_FS_MINIMIZE'))
ffconfig.set('FF_USE_FIND', get_option('FATFS_USE_FIND'))
ffconfig.set('FF_USE_MKFS', get_option('FATFS_USE_MKFS'))
ffconfig.set('FF_USE_FASTSEEK', get_option('FATFS_USE_FASTSEEK'))
ffconfig.set('FF_USE_EXPAND', get_option('FATFS_USE_EXPAND'))
ffconfig.set('FF_USE_CHMOD', get_option('FATFS_USE_CHMOD'))
ffconfig.set('FF_USE_LABEL', get_option('FATFS_USE_LABEL'))
ffconfig.set('FF_USE_FORWARD', get_option('FATFS_USE_FORWARD'))
ffconfig.set('FF_USE_STRFUNC', get_option('FATFS_USE_STRFUNC'))
ffconfig.set('FF_PRINT_LLI', get_option('FATFS_PRINT_LLI'))
ffconfig.set('FF_PRINT_FLOAT', get_option('FATFS_PRINT_FLOAT'))
ffconfig.set('FF_STRF_ENCODE', get_option('FATFS_STRF_ENCODE'))

# Locale and Namespace Configurations
ffconfig.set('FF_CODE_PAGE', get_option('FATFS_CODE_PAGE'))
ffconfig.set('FF_USE_LFN', get_option('FATFS_USE_LFN'))
ffconfig.set('FF_LFN_UNICODE', get_option('FATFS_LFN_UNICODE'))
ffconfig.set('FF_FS_RPATH', get_option('FATFS_FS_RPATH'))

# Drive/Volume Configurations
ffconfig.set('FF_VOLUMES', get_option('FATFS_VOLUMES'))
ffconfig.set('FF_STR_VOLUME_ID', get_option('FATFS_STR_VOLUME_ID'))
ffconfig.set('FF_MULTI_PARTITION', get_option('FATFS_MULTI_PARTITION'))
ffconfig.set('FF_MIN_SS', get_option('FATFS_MIN_SS'))
ffconfig.set('FF_MAX_SS', get_option('FATFS_MAX_SS'))
ffconfig.set('FF_USE_TRIM', get_option('FATFS_USE_TRIM'))

# System Configurations
ffconfig.set('FF_FS_TINY', get_option('FATFS_FS_TINY'))
ffconfig.set('FF_FS_EXFAT', get_option('FATFS_FS_EXFAT'))
ffconfig.set('FF_FS_NORTC', get_option('FATFS_FS_NORTC'))
ffconfig.set('FF_FS_NOFSINFO', get_option('FATFS_FS_NOFSINFO'))
ffconfig.set('FF_FS_LOCK', get_option('FATFS_FS_LOCK'))
ffconfig.set('FF_FS_REENTRANT', get_option('FATFS_FS_REENTRANT'))
ffconfig.set('FF_FS_TIMEOUT', get_option('FATFS_FS_TIMEOUT'))

# Generate configuration header
configure_file(
  input : 'config/ffconf.h.in',
  output : 'ffconf.h',
  configuration : ffconfig
)



fatfs_inc = include_directories(
        'include',
)

fatfs_config = include_directories(
        'config',
)

fatfs_src = files(
    'source/ff.c',
    'source/ffunicode.c',
)


fatfs_lib = static_library(
    'fatfs',
    sources: [fatfs_src],
    include_directories: [
        fatfs_inc,
        fatfs_config,
    ],
    c_args: [
        common_cflags,
        '-DFFCONF_DEF=5380',  # Default configuration
    ],
    native: false,
)

# fatfs_native_lib = static_library(
#     'fatfs_native',
#     sources: [fatfs_src],
#     include_directories: [
#         fatfs_inc,
#         fatfs_config,
#     ],
#     c_args: [common_cflags,
#     '-DFF_MULTI_PARTITION=0',  # Disable multi-partition support
#     ],
#     native: true,
# )

fatfs_dep = declare_dependency(
    # sources: fatfs_rtos_src,
    include_directories: fatfs_inc,
    link_with: fatfs_lib,
    compile_args: [common_cflags],
)

# fatfs_native_dep = declare_dependency(
#     # sources: fatfs_native_src,
#     include_directories: fatfs_inc,
#     link_with: fatfs_native_lib,
#     compile_args: [common_cflags],
# )