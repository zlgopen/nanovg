import os
import platform

def joinPath(root, subdir):
  return os.path.normpath(os.path.join(root, subdir))

OS_NAME=platform.system()
PACKAGE_ROOT = os.path.normpath(os.getcwd())
PACKAGE_SRC = joinPath(PACKAGE_ROOT, 'src')
PACKAGE_3RD_ROOT = joinPath(PACKAGE_ROOT, '3rd')
BIN_DIR=joinPath(PACKAGE_ROOT, 'bin')
LIB_DIR=joinPath(PACKAGE_ROOT, 'lib')

os.environ['BIN_DIR'] = BIN_DIR;
os.environ['LIB_DIR'] = LIB_DIR;

COMMON_CCFLAGS=' -DHAS_STDIO -DSTBTT_STATIC -DSTB_IMAGE_STATIC '

OS_LIBS=[]
OS_LIBPATH=[]
OS_CPPPATH=[]
OS_LINKFLAGS=''
OS_FLAGS='-g -Wall'
OS_SUBSYSTEM_CONSOLE=''
OS_SUBSYSTEM_WINDOWS=''
OS_PROJECTS=[]

if OS_NAME == 'Darwin':
  OS_LINKFLAGS='-framework OpenGL'
  COMMON_CCFLAGS = COMMON_CCFLAGS + ' -D__APPLE__ -DHAS_PTHREAD -DMACOS '
  OS_LIBS = OS_LIBS + ['stdc++', 'pthread', 'm', 'dl']

elif OS_NAME == 'Linux':
  OS_LIBS = ['GL'] + OS_LIBS + ['stdc++', 'pthread', 'm', 'dl']
  COMMON_CCFLAGS = COMMON_CCFLAGS + ' -DLINUX -DHAS_PTHREAD'
  OS_PROJECTS=['3rd/SDL/SConscript']

elif OS_NAME == 'Windows':
  OS_LIBS=['gdi32', 'user32','winmm.lib','imm32.lib','version.lib','shell32.lib','ole32.lib','Oleaut32.lib','Advapi32.lib']
  OS_FLAGS='-DWIN32 -D_WIN32 -DWINDOWS /EHsc -D_CONSOLE  /DEBUG /Od /ZI'
  OS_LINKFLAGS='/MACHINE:X64 /DEBUG'
  OS_SUBSYSTEM_CONSOLE='/SUBSYSTEM:CONSOLE  '
  OS_SUBSYSTEM_WINDOWS='/SUBSYSTEM:WINDOWS  '
  OS_PROJECTS=['3rd/SDL/SConscript']

LINKFLAGS=OS_LINKFLAGS;
LIBPATH=[LIB_DIR] + OS_LIBPATH
CCFLAGS=OS_FLAGS + COMMON_CCFLAGS 
LIBS=['nanovg'] + OS_LIBS

CPPPATH=[PACKAGE_ROOT, PACKAGE_SRC,  PACKAGE_3RD_ROOT] + OS_CPPPATH

DefaultEnvironment(CCFLAGS = CCFLAGS, 
  LIBS = LIBS,
  LIBPATH = LIBPATH,
  CPPPATH = CPPPATH,
  LINKFLAGS = LINKFLAGS,
  OS_SUBSYSTEM_CONSOLE=OS_SUBSYSTEM_CONSOLE,
  OS_SUBSYSTEM_WINDOWS=OS_SUBSYSTEM_WINDOWS
)

SConscript(['SConscript'])

