# Bibble

# Installation
Installation is very straightforward.

## Windows
No.

## Debian / Ubuntu
### X86-64
```shell
curl -fL https://github.com/JannikBulow/Bibble/releases/download/v0.1.0/bibble_0.1.0_amd64.deb -o /tmp/bibble.deb && sudo apt install /tmp/bibble.deb
```

### To uninstall
```shell
sudo apt remove bibble
```

### ARM
There is no official arm build. See [Build from source](#build-from-source)

## Arch
AUR account creation is temporarily down. But the package will be named `bibble`.

## MacOS
No.

## Build from source
Requires CMake, NASM and your favorite C++ compiler.

```shell
git clone https://github.com/JannikBulow/Bibble.git && cmake -S Bibble -B Bibble/build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local && cmake --build Bibble/build -j && sudo cmake --install Bibble/build
```