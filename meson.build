project('fatfs', 'c', version: 'v0.15')

common_cflags = [
    '-Wno-conversion',
    '-Wno-pedantic',
    '-Wno-sign-conversion',
    '-Wno-comment',
    '-Wno-switch-enum',
    '-Wno-unused-parameter',
]

fatfs_inc = include_directories(
        'config',
        'source',
)

fatfs_src = files(
    'source/ff.c',
    'source/ffunicode.c',
)

fatfs_rtos_src = files(
    'source/ffsystem_rtos.c',
)

fatfs_native_src = files(
    'source/ffsystem_linux.c',
)

fatfs_lib = static_library(
    'fatfs',
    sources: [fatfs_src],
    include_directories: [
        fatfs_inc,
    ],
    c_args: common_cflags,
    native: false,
)

fatfs_native_lib = static_library(
    'fatfs_native',
    sources: [fatfs_src],
    include_directories: [
        fatfs_inc,
    ],
    c_args: [common_cflags,
    '-DFF_MULTI_PARTITION=0',  # Disable multi-partition support
    ],
    native: true,
)

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