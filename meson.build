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
message('Configuring FatFs library')
message(get_option('FATFS_CODE_PAGE'))

# FATFS REV version
ffconfig.set('FATFS_FFCONF_DEF', '5380')

# Function Configurations
if get_option('FATFS_FS_READONLY')
    message('FATFS_FS_READONLY')
    ffconfig.set('FATFS_FF_FS_READONLY', 1)
else
    ffconfig.set('FATFS_FF_FS_READONLY', 0)
endif

ffconfig.set('FATFS_FF_FS_MINIMIZE', get_option('FATFS_FS_MINIMIZE'))
ffconfig.set('FATFS_FF_USE_FIND', get_option('FATFS_USE_FIND'))

if get_option('FATFS_USE_MKFS')
    message('FATFS_USE_MKFS')
    ffconfig.set('FATFS_FF_USE_MKFS', 1)
else
    ffconfig.set('FATFS_FF_USE_MKFS', 0)
endif

if get_option('FATFS_USE_FASTSEEK')
    message('FATFS_USE_FASTSEEK')
    ffconfig.set('FATFS_FF_USE_FASTSEEK', 1)
else
    ffconfig.set('FATFS_FF_USE_FASTSEEK', 0)
endif

if get_option('FATFS_USE_EXPAND')
    message('FATFS_USE_EXPAND')
    ffconfig.set('FATFS_FF_USE_EXPAND', 1)
else
    ffconfig.set('FATFS_FF_USE_EXPAND', 0)
endif

if get_option('FATFS_USE_CHMOD')
    message('FATFS_USE_CHMOD')
    ffconfig.set('FATFS_FF_USE_CHMOD', 1)
else
    ffconfig.set('FATFS_FF_USE_CHMOD', 0)
endif

if get_option('FATFS_USE_LABEL')
    message('FATFS_USE_LABEL')
    ffconfig.set('FATFS_FF_USE_LABEL', 1)
else
    ffconfig.set('FATFS_FF_USE_LABEL', 0)
endif

if get_option('FATFS_USE_FORWARD')
    message('FATFS_USE_FORWARD')
    ffconfig.set('FATFS_FF_USE_FORWARD', 1)
else
    ffconfig.set('FATFS_FF_USE_FORWARD', 0)
endif

ffconfig.set('FATFS_FF_USE_STRFUNC', get_option('FATFS_USE_STRFUNC'))

if get_option('FATFS_PRINT_LLI')
    message('FATFS_PRINT_LLI')
    ffconfig.set('FATFS_FF_PRINT_LLI', 1)
else
    ffconfig.set('FATFS_FF_PRINT_LLI', 0)
endif

if get_option('FATFS_PRINT_FLOAT')
    message('FATFS_PRINT_FLOAT')
    ffconfig.set('FATFS_FF_PRINT_FLOAT', 1)
else
    ffconfig.set('FATFS_FF_PRINT_FLOAT', 0)
endif

ffconfig.set('FATFS_FF_STRF_ENCODE', get_option('FATFS_STRF_ENCODE'))

# Locale and Namespace Configurations
ffconfig.set('FATFS_FF_CODE_PAGE', get_option('FATFS_CODE_PAGE'))
ffconfig.set('FATFS_FF_USE_LFN', get_option('FATFS_USE_LFN'))
ffconfig.set('FATFS_FF_LFN_UNICODE', get_option('FATFS_LFN_UNICODE'))
ffconfig.set('FATFS_FF_FS_RPATH', get_option('FATFS_FS_RPATH'))

# Drive/Volume Configurations
ffconfig.set('FATFS_FF_VOLUMES', get_option('FATFS_VOLUMES'))

if get_option('FATFS_STR_VOLUME_ID')
    message('FATFS_STR_VOLUME_ID')
    ffconfig.set('FATFS_FF_STR_VOLUME_ID', 1)
else
    ffconfig.set('FATFS_FF_STR_VOLUME_ID', 0)
endif

if get_option('FATFS_MULTI_PARTITION')
    message('FATFS_MULTI_PARTITION')
    ffconfig.set('FATFS_FF_MULTI_PARTITION', 1)
else
    ffconfig.set('FATFS_FF_MULTI_PARTITION', 0)
endif


ffconfig.set('FATFS_FF_MIN_SS', get_option('FATFS_MIN_SS'))
ffconfig.set('FATFS_FF_MAX_SS', get_option('FATFS_MAX_SS'))

if get_option('FATFS_USE_TRIM')
    message('FATFS_USE_TRIM')
    ffconfig.set('FATFS_FF_USE_TRIM', 1)
else
    ffconfig.set('FATFS_FF_USE_TRIM', 0)
endif


# System Configurations
if get_option('FATFS_FS_TINY')
    message('FATFS_FS_TINY')
    ffconfig.set('FATFS_FF_FS_TINY', 1)
else
    ffconfig.set('FATFS_FF_FS_TINY', 0)
endif

if get_option('FATFS_FS_EXFAT')
    message('FATFS_FS_EXFAT')
    ffconfig.set('FATFS_FF_FS_EXFAT', 1)
else
    ffconfig.set('FATFS_FF_FS_EXFAT', 0)
endif
if get_option('FATFS_FS_NORTC')
    message('FATFS_FS_NORTC')
    ffconfig.set('FATFS_FF_FS_NORTC', 1)
else
    ffconfig.set('FATFS_FF_FS_NORTC', 0)
endif


ffconfig.set('FATFS_FF_FS_NOFSINFO', get_option('FATFS_FS_NOFSINFO'))
ffconfig.set('FATFS_FF_FS_LOCK', get_option('FATFS_FS_LOCK'))
if get_option('FATFS_FS_REENTRANT')
    message('FATFS_FS_REENTRANT')
    ffconfig.set('FATFS_FF_FS_REENTRANT', 1)
else
    ffconfig.set('FATFS_FF_FS_REENTRANT', 0)
endif

ffconfig.set('FATFS_FF_FS_TIMEOUT', get_option('FATFS_FS_TIMEOUT'))

# Generate configuration header
configure_file(
  input : 'config/ffconf.h.in',
  output : 'ffconf.h',
  configuration : ffconfig
)



fatfs_inc = include_directories(
    '.',
    'include',
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