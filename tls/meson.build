# Meson file for Vibe TLS

vibe_tls_src_dir = include_directories('.')

vibe_tls_src = [
    'vibe/stream/botan.d',
    'vibe/stream/openssl.d',
    'vibe/stream/tls.d'
]

#
# Install Includes
#
install_subdir('vibe/', install_dir: 'include/d/vibe/')

#
# Build Targets
#

# TLS stream implementations
vibe_tls_lib = library('vibe-tls',
        [vibe_tls_src],
        dependencies: [vibe_utils_dep,
                       vibe_stream_dep,
                      ],
        install: true,
        pic: true,
        version: project_version,
        soversion: project_soversion,
        d_module_versions: ['VibeNoSSL']
)
pkgc.generate(vibe_tls_lib,
              subdirs: 'd/vibe',
              requires: ['vibe-stream'],
              version: project_version,
              d_module_versions: ['VibeNoSSL'],
              description: 'TLS stream implementations for Vibe.'
)

vibe_tls_dep = declare_dependency(
    link_with: [vibe_tls_lib],
    include_directories: [vibe_tls_src_dir],
    dependencies: [vibe_stream_dep],
    d_module_versions: ['VibeNoSSL']
)

#
# Tests
#
vibe_test_tls_exe = executable('vibe-test_tls',
    [vibe_tls_src],
    dependencies: [vibe_utils_dep,
                   vibe_stream_dep,
                  ],
    d_unittest: true,
    link_args: '--main'
)
test('vibe-test_tls', vibe_test_tls_exe)
