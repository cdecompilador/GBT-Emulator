# GameBoy Twitch - Un emulador desarrollado totalmente en vivo desde Twitch

![](https://pbs.twimg.com/media/EwjBnsWWYAYIw0o?format=jpg&name=medium)

## ES
En este repositorio encontraréis el avance del emulador de Gameboy que desarrollamos en mi [canal de Twitch](https://twitch.tv/AbdeCreativeDev).

### Requisitos:

- `cmake`
- `vcpkg` (para descargar y compilar sdl2)

### Uso

Primero descargamos y configuramos vcpkg, [¿Como se hace esto?](https://github.com/microsoft/vcpkg/blob/master/README_es.md#inicio-r%C3%A1pido-windows)
Instalamos y compilamos sdl2, aseguraos que termina sin ningún error.
```shell
vcpkg install sdl2:x64-windows
```
El [triplet](https://wiki.osdev.org/Target_Triplet) `x64-windows` no es necesario que lo tengáis que poner, si tenéis un sistema de 32-bits usad `x86-windows`, o si usáis otro sistema operativo `x64-linux` / `x64-osx`


Luego hacemos:
```shell
vcpkg integrate install
```
Lo cual nos devolverá lo siguiente:
```shell
Applied user-wide integration for this vcpkg root.

CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=.../vcpkg/scripts/buildsystems/vcpkg.cmake"
```
Luego cuando usemos cmake si le pasamos lo siguiente como variable `"-DCMAKE_TOOLCHAIN_FILE=.../vcpkg/scripts/buildsystems/vcpkg.cmake"` sabrá como buscar sdl2 dentro de vcpkg con facilidad, esto nos automatizará el linkage y demás con la librería.

Ahora ya dentro de la carpeta de nustro proyecto creamos la carpeta donde compilaremos el ejecutable,
en mi caso `build`
```shell
mkdir build
cd build
```

Ahora ejecutamos cmake, como este nos da una gran variedad de posibilidades dejaré aqui las más comununes y testeadas por los desarrolladores.

**En Windows** (con **MSVC**, no hay que decirle nada más ya que MSVC es el compilador por defecto y msbuild el
build system por defecto en windows):
```shell
cmake "-DCMAKE_TOOLCHAIN_FILE=.../vcpkg/scripts/buildsystems/vcpkg.cmake" ..
cmake --build . --target Release
```
MSVC(y XCode) ya generan por defecto los targets de `Debug`, `Release`, `RelWithDebInfo` y `MinSizeRel` 
el resto de build systems se deben generar para un target en específico pasandole a cmake a la hora
de generar el build system `-DCMAKE_BUILD_TYPE=Debug|Release|RelWithDebInfo|MinSizeRel` o puedes crear
un target customizado (si tienes que usar sse o avx por ejemplo)

**En Windows (con clang):**
```shell
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=clang "-DCMAKE_TOOLCHAIN_FILE=..." -G "Unix Makefiles" ..
cmake --build .
```

**En Linux** (con con que esté en la variable en entorno $(CC), normalmente **gcc**):
```shell
cmake -DCMAKE_BUILD_TYPE=Release "-DCMAKE_TOOLCHAIN_FILE=..." ..
make # o cmake --build .
```

**En MacOS (clang usando ninja)**:
```shell
cmake -DCMAKE_C_COMPILER=clang -DCMAKE_BUILD_TYPE=Release "-DCMAKE_TOOLCHAIN_FILE=..." -G "Ninja" ..
cmake --build . # o ninja
```
TODO...
### Recursos

Este emulador está basado en estos recursos (lista no exhaustiva): 

- [GB CPU Manual](http://marc.rawer.de/Gameboy/Docs/GBCPUman.pdf)
- [GB Pandocs](https://gbdev.io/pandocs/)
- [Gameboy Talks](https://www.retroreversing.com/gameboy/hardware)
- [GGB - A Game Boy emulator written in C++](https://github.com/geaz/emu-gameboy) -> hemos generado las instrucciones de los opcodes gracias a este proyecto
- [Imran Nazar: Gameboy Emulation in JavaScript](http://imrannazar.com/GameBoy-Emulation-in-JavaScript)
- [The Ultimate GameBoy talk (33c3)](https://www.youtube.com/watch?v=HyzD8pNlpwI)
- [The Game Boy: a hardware architecture](https://www.youtube.com/watch?v=RZUDEaLa5Nw)
- [Memory mapping](http://gameboy.mongenel.com/dmg/asmmemmap.html)

******

## EN
In this repository you will find the progress done on the Gameboy emulator that I am developing live on my [Twitch channel](https://twitch.tv/AbdeCreativeDev).

### Requirements:

- cmake 
- vcpkg

### Usage
TODO...
### Resources 

This emulator is based on the following resources (list is not exhaustive): 

- [GB CPU Manual](http://marc.rawer.de/Gameboy/Docs/GBCPUman.pdf)
- [GB Pandocs](https://gbdev.io/pandocs/)
- [Gameboy Talks](https://www.retroreversing.com/gameboy/hardware)
- [GGB - A Game Boy emulator written in C++](https://github.com/geaz/emu-gameboy) -> we have generated the instruction set from the opcode table thanks to this project
- [Imran Nazar: Gameboy Emulation in JavaScript](http://imrannazar.com/GameBoy-Emulation-in-JavaScript)
- [The Ultimate GameBoy talk (33c3)](https://www.youtube.com/watch?v=HyzD8pNlpwI)
- [The Game Boy: a hardware architecture](https://www.youtube.com/watch?v=RZUDEaLa5Nw)
