project(
    'bencode2',
    'cpp',
    default_options: [
        'c_std=c17',
        'cpp_std=c++20',
        'buildtype=release',
        'debug=false',
    ],
    meson_version: '>= 1.3.0',
)

py = import('python').find_installation(pure: false)

py.install_sources(
    'src/bencode2/__init__.py',
    'src/bencode2/__init__.pyi',
    'src/bencode2/__bencode.pyi',
    'src/bencode2/__encoder.py',
    'src/bencode2/__decoder.py',
    'src/bencode2/py.typed',
    subdir: 'bencode2',
)

add_project_arguments('-DFMT_HEADER_ONLY', language: 'cpp')

nanobind_dep = dependency('nanobind', static: true)


out = py.extension_module(
    '__bencode',
    'src/bencode2/bencode.cpp',
    'src/bencode2/encode.cpp',
    'src/bencode2/decode.cpp',
    install: true,
    include_directories: include_directories(
        './vendor/small_vector/source/include/',
        './vendor/fmt/include/',
    ),
    subdir: 'bencode2',
    dependencies: [nanobind_dep, py.dependency()],
    limited_api: '3.12',
)
