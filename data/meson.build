# Meson file for Vibe Data

vibe_data_src_dir = include_directories('.')

vibe_data_src = [
    'vibe/data/bson.d',
    'vibe/data/json.d',
    'vibe/data/serialization.d'
]

#
# Install Includes
#
install_subdir('vibe/', install_dir: 'include/d/vibe/')

#
# Build Targets
#

# Data format and serialization support
vibe_data_lib = library('vibe-data',
        [vibe_data_src],
        install: true,
        pic: true,
        dependencies: [vibe_utils_dep],
        version: project_version,
        soversion: project_soversion
)

pkgc.generate(vibe_data_lib,
              subdirs: 'd/vibe',
              version: project_version,
              requires: ['vibe-utils'],
              description: 'Data format and serialization support for Vibe.'
)

vibe_data_dep = declare_dependency(
    link_with: [vibe_data_lib],
    include_directories: [vibe_data_src_dir],
    dependencies: [vibe_utils_dep]
)

#
# Tests
#
vibe_test_data_exe = executable('vibe-test_data',
    [vibe_data_src],
    include_directories: [vibe_utils_src_dir],
    dependencies: [vibe_utils_dep],
    d_unittest: true,
    link_args: '--main'
)
test('vibe-test_data', vibe_test_data_exe)
