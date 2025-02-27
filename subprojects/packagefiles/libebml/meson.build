project('libebml', 'cpp',
  version : '1.4.2',
  default_options : ['warning_level=1', 'cpp_std=c++14']
)

#hacks to fix compilation with GCC11. They go away with the next version
#run_command('sed', 's/cassert/limits/g', '-i', 'src/EbmlString.cpp', check : true)
#run_command('sed', 's/cassert/limits/g', '-i', 'src/EbmlUnicodeString.cpp', check : true)

cpp = meson.get_compiler('cpp')
if cpp.get_id() == 'msvc'
  ebml_conf = configure_file(output: 'ebml_export.h', configuration: {'EBML_DLL_API': '__declspec(dllexport)'})
else
  ebml_conf = configure_file(output: 'ebml_export.h', configuration: {'EBML_DLL_API': ''})
endif

libebml_incdir = include_directories(['.'])

install_headers(
  'ebml/Debug.h',
  'ebml/EbmlBinary.h',
  'ebml/EbmlConfig.h',
  'ebml/EbmlContexts.h',
  'ebml/EbmlCrc32.h',
  'ebml/EbmlDate.h',
  'ebml/EbmlDummy.h',
  'ebml/EbmlElement.h',
  'ebml/EbmlEndian.h',
  'ebml/EbmlFloat.h',
  'ebml/EbmlHead.h',
  'ebml/EbmlId.h',
  'ebml/EbmlMaster.h',
  'ebml/EbmlSInteger.h',
  'ebml/EbmlStream.h',
  'ebml/EbmlString.h',
  'ebml/EbmlSubHead.h',
  'ebml/EbmlTypes.h',
  'ebml/EbmlUInteger.h',
  'ebml/EbmlUnicodeString.h',
  'ebml/EbmlVersion.h',
  'ebml/EbmlVoid.h',
  'ebml/IOCallback.h',
  'ebml/MemIOCallback.h',
  'ebml/MemReadIOCallback.h',
  'ebml/SafeReadIOCallback.h',
  'ebml/StdIOCallback.h',
  ebml_conf,
  subdir : 'ebml',
)

libebml = static_library('libebml',
  'src/Debug.cpp',
  'src/EbmlBinary.cpp',
  'src/EbmlContexts.cpp',
  'src/EbmlCrc32.cpp',
  'src/EbmlDate.cpp',
  'src/EbmlDummy.cpp',
  'src/EbmlElement.cpp',
  'src/EbmlFloat.cpp',
  'src/EbmlHead.cpp',
  'src/EbmlMaster.cpp',
  'src/EbmlSInteger.cpp',
  'src/EbmlStream.cpp',
  'src/EbmlString.cpp',
  'src/EbmlSubHead.cpp',
  'src/EbmlUInteger.cpp',
  'src/EbmlUnicodeString.cpp',
  'src/EbmlVersion.cpp',
  'src/EbmlVoid.cpp',
  'src/IOCallback.cpp',
  'src/MemIOCallback.cpp',
  'src/MemReadIOCallback.cpp',
  'src/SafeReadIOCallback.cpp',
  'src/StdIOCallback.cpp',
  include_directories : libebml_incdir,
  install : true,
)

pkg = import('pkgconfig')
pkg.generate(libebml)

libebml_dep = declare_dependency(
  include_directories : libebml_incdir,
  link_with : libebml,
)
