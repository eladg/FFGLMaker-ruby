# FFGLMaker

Quick and easy script to generate a FFGL plugins using [GLSL Sandbox](http://glslsandbox.com) and [ShaderToy](https://www.shadertoy.com) shaders. FFGLMaker supports OS X only (although may work on other environments). Tested on: [Resolume Avenue 4.5.0](https://resolume.com/software).

NO INSTALLATION OF XCODE OR PROGRAMING KNOWLEDGE REQUIRED.

Related Repos:
- [ShaderMaker](https://github.com/leadedge/ShaderMaker) - FFGL Plugin Template.
- [ShaderMaker-FFGLMakerTemplate](https://github.com/eladg/ShaderMaker-FFGLMakerTemplate) - The template that FFGLMaker will be using.

### Installation

This is a simple [ruby](https://www.ruby-lang.org) script based on [Thor](https://github.com/erikhuda/thor) command-line interface and ERB templates.
No formal installation at this point, for now you're own your own.

Please submit any questions to: [@eladg](https://twitter.com/elad_g)

Dependencies: [Thor](https://github.com/erikhuda/thor), [ERB](http://ruby-doc.org/stdlib-2.2.3/libdoc/erb/rdoc/ERB.html), Xcode Command Line tools (for compiling the plugin)

### Usage
```
Usage:
  FFGLMaker.rb Create -i, --shader=SHADER -n, --name=NAME

Options:
  -i, --shader=SHADER                      # Shader input text file path
  -n, --name=NAME                          # Desired name of the FFGL Plugin
  -s, [--source-plug], [--no-source-plug]  # Generate a 'source' FFGL plugin rather then an 'effect'

Description:
  Generate and compile a given shader file (sourced from GLSL Sandbox or ShaderToy) to an FFGL Plugin. The bundled plugin will be generated under the build/release folder.
```

### Runtime Example

1. Compose/browse for a shader you like and save it to a file on your desktop, say: `~/Desktop/shader.txt`
2. Open terminal and navigate to `FFGLMaker` folder.
3. Execute `./FFGLMaker.rb -s -i ~/desktop/shader.txt -n "FFGL My Shader" `
  - `-s` Mark this shader as SOURCE rather then an EFFECT plugin.
  - `-i` Input shader file.
  - `-n` Name of the new plugin.
4. Plugin will be generated on: `<< FFGLMaker Folder >>/build/release/<< PLUGIN NAME >>.bundle`
5. Place the generated plugin on VFX folder or your favoirate FFGL plugin folder []

Log Dump (will be better soon, I promise):
```
elad:~/Documents/eladg/FFGLMaker$ ./FFGLMaker.rb -s -i ~/desktop/shader.txt -n "FFGL My Shader"

------------------------------------
  Compilation Text Start
------------------------------------

rm -rf FFGLPluginInfo.o FFGLPluginInfoData.o FFGL.o FFGLShader.o FFGLExtensions.o FFGLPluginManager.o FFGLPluginSDK.o ShaderMaker.o *.dylib
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o ShaderMaker.o ../../ShaderMaker.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLPluginInfo.o ../../FFGL/FFGLPluginInfo.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLPluginInfoData.o ../../FFGL/FFGLPluginInfoData.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGL.o ../../FFGL/FFGL.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLShader.o ../../FFGL/FFGLShader.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLExtensions.o ../../FFGL/FFGLExtensions.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLPluginManager.o ../../FFGL/FFGLPluginManager.cpp
clang++ -c -Wall -Wno-unknown-pragmas -pedantic -I../../ -I../../FFGL -DTARGET_OS_MAC -std=c++11 -stdlib=libc++ -arch x86_64 -arch i386 -g0 -Os -o FFGLPluginSDK.o ../../FFGL/FFGLPluginSDK.cpp
clang++ -o ShaderMaker.dylib -dynamiclib -framework GLUT -framework OpenGL -arch x86_64 -arch i386 FFGLPluginInfo.o FFGLPluginInfoData.o FFGL.o FFGLShader.o FFGLExtensions.o FFGLPluginManager.o FFGLPluginSDK.o ShaderMaker.o
rm -rf "../../Binaries/osx/ShaderMaker.bundle"
mkdir -p "../../Binaries/osx/ShaderMaker.bundle"/Contents/MacOS
cp Info.plist "../../Binaries/osx/ShaderMaker.bundle/Contents"
mv ./ShaderMaker.dylib "../../Binaries/osx/ShaderMaker.bundle/Contents/MacOS/ShaderMaker"
../../ShaderMaker.cpp:85:26: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
char *vertexShaderCode = STRINGIFY (
                         ^
../../ShaderMaker.cpp:64:22: note: expanded from macro 'STRINGIFY'
#define STRINGIFY(A) #A
                     ^
<scratch space>:398:1: note: expanded from here
"void main() { gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex; gl_TexCoord[0] = gl_MultiTexCoord0; gl_FrontColor = gl_Color; }"
^
../../ShaderMaker.cpp:129:2: warning: embedding a directive within macro arguments has undefined behavior [-Wembedded-directive]
#ifdef GL_ES
 ^
../../ShaderMaker.cpp:122:28: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
char *fragmentShaderCode = STRINGIFY (
                           ^
../../ShaderMaker.cpp:64:22: note: expanded from macro 'STRINGIFY'
#define STRINGIFY(A) #A
                     ^
<scratch space>:398:1: note: expanded from here
"uniform float time; uniform vec2 mouse; uniform vec2 resolution; void main( void ) { vec2 uv = ( gl_FragCoord.xy / resolution.xy ) * 2.0 - 1.0; float t = abs( 1.0 / (sin( uv.y + sin( time + uv.x * 10.0 ) * uv.x ) * 10.0) ); vec3 finalColor = vec3( t * 0.2, t * 0.2, t * 0.9 ); gl_FragColor = vec4( finalColor, 95.0 ); }"
^
../../ShaderMaker.cpp:807:34: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                static char *extraUniforms = { "uniform vec4 inputColour;\n" };
                                               ^
../../ShaderMaker.cpp:828:30: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                        static char *uniforms = { "uniform vec3 iResolution;\n"
                                                  ^
../../ShaderMaker.cpp:851:39: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                                static char *stoyMainFunction = { "void main(void) {\n"
                                                                  ^
6 warnings generated.
../../ShaderMaker.cpp:85:26: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
char *vertexShaderCode = STRINGIFY (
                         ^
../../ShaderMaker.cpp:64:22: note: expanded from macro 'STRINGIFY'
#define STRINGIFY(A) #A
                     ^
<scratch space>:398:1: note: expanded from here
"void main() { gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex; gl_TexCoord[0] = gl_MultiTexCoord0; gl_FrontColor = gl_Color; }"
^
../../ShaderMaker.cpp:129:2: warning: embedding a directive within macro arguments has undefined behavior [-Wembedded-directive]
#ifdef GL_ES
 ^
../../ShaderMaker.cpp:122:28: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
char *fragmentShaderCode = STRINGIFY (
                           ^
../../ShaderMaker.cpp:64:22: note: expanded from macro 'STRINGIFY'
#define STRINGIFY(A) #A
                     ^
<scratch space>:398:1: note: expanded from here
"uniform float time; uniform vec2 mouse; uniform vec2 resolution; void main( void ) { vec2 uv = ( gl_FragCoord.xy / resolution.xy ) * 2.0 - 1.0; float t = abs( 1.0 / (sin( uv.y + sin( time + uv.x * 10.0 ) * uv.x ) * 10.0) ); vec3 finalColor = vec3( t * 0.2, t * 0.2, t * 0.9 ); gl_FragColor = vec4( finalColor, 95.0 ); }"
^
../../ShaderMaker.cpp:807:34: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                static char *extraUniforms = { "uniform vec4 inputColour;\n" };
                                               ^
../../ShaderMaker.cpp:828:30: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                        static char *uniforms = { "uniform vec3 iResolution;\n"
                                                  ^
../../ShaderMaker.cpp:851:39: warning: ISO C++11 does not allow conversion from string literal to 'char *' [-Wwritable-strings]
                                static char *stoyMainFunction = { "void main(void) {\n"
                                                                  ^
6 warnings generated.
../../FFGL/FFGLExtensions.cpp:60:7: warning: 'NSIsSymbolNameDefined' is deprecated: first deprecated in OS X 10.4 [-Wdeprecated-declarations]
  if (NSIsSymbolNameDefined(symbolName))
      ^
/usr/include/mach-o/dyld.h:169:17: note: 'NSIsSymbolNameDefined' has been explicitly marked deprecated here
extern bool     NSIsSymbolNameDefined(const char* symbolName)                                                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_4,__IPHONE_NA,__IPHONE_NA);
                ^
../../FFGL/FFGLExtensions.cpp:61:14: warning: 'NSLookupAndBindSymbol' is deprecated: first deprecated in OS X 10.4 [-Wdeprecated-declarations]
    symbol = NSLookupAndBindSymbol(symbolName);
             ^
/usr/include/mach-o/dyld.h:172:17: note: 'NSLookupAndBindSymbol' has been explicitly marked deprecated here
extern NSSymbol NSLookupAndBindSymbol(const char* symbolName)                                                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_4,__IPHONE_NA,__IPHONE_NA);
                ^
../../FFGL/FFGLExtensions.cpp:65:12: warning: 'NSAddressOfSymbol' is deprecated: first deprecated in OS X 10.5 [-Wdeprecated-declarations]
    return NSAddressOfSymbol(symbol);
           ^
/usr/include/mach-o/dyld.h:181:21: note: 'NSAddressOfSymbol' has been explicitly marked deprecated here
extern void *       NSAddressOfSymbol(NSSymbol symbol) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
                    ^
3 warnings generated.
../../FFGL/FFGLExtensions.cpp:60:7: warning: 'NSIsSymbolNameDefined' is deprecated: first deprecated in OS X 10.4 [-Wdeprecated-declarations]
  if (NSIsSymbolNameDefined(symbolName))
      ^
/usr/include/mach-o/dyld.h:169:17: note: 'NSIsSymbolNameDefined' has been explicitly marked deprecated here
extern bool     NSIsSymbolNameDefined(const char* symbolName)                                                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_4,__IPHONE_NA,__IPHONE_NA);
                ^
../../FFGL/FFGLExtensions.cpp:61:14: warning: 'NSLookupAndBindSymbol' is deprecated: first deprecated in OS X 10.4 [-Wdeprecated-declarations]
    symbol = NSLookupAndBindSymbol(symbolName);
             ^
/usr/include/mach-o/dyld.h:172:17: note: 'NSLookupAndBindSymbol' has been explicitly marked deprecated here
extern NSSymbol NSLookupAndBindSymbol(const char* symbolName)                                                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_4,__IPHONE_NA,__IPHONE_NA);
                ^
../../FFGL/FFGLExtensions.cpp:65:12: warning: 'NSAddressOfSymbol' is deprecated: first deprecated in OS X 10.5 [-Wdeprecated-declarations]
    return NSAddressOfSymbol(symbol);
           ^
/usr/include/mach-o/dyld.h:181:21: note: 'NSAddressOfSymbol' has been explicitly marked deprecated here
extern void *       NSAddressOfSymbol(NSSymbol symbol) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
                    ^
3 warnings generated.

------------------------------------
  Compilation Text End
------------------------------------

Plugin Created on: build/release/FFGL_My_Shader.bundle

Done.

```

### Nice Ideas

I got lots of idea and some free time. Shot them at me to [@eladg](https://twitter.com/elad_g)

### License
The MIT License (MIT)

PLEASE READ LICENSE FILE INCLUDED IN THIS REPO
