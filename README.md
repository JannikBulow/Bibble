# Bibble

# Installation
Installation is very straightforward.

## Windows
No.

## Debian / Ubuntu
### X86-64
```shell
curl -fL https://github.com/JannikBulow/Bibble/releases/download/v0.1.0/bibble_0.1.0_x86_64.deb -o /tmp/bibble.deb && sudo apt install /tmp/bibble.deb
```

### ARM
There is no official arm build. See [Build from source](#build-from-source)

### To uninstall
```shell
sudo apt remove bibble
```

## Arch
It should soon be on the AUR, but I still recommend downloading from this repository as the AUR is known to be full of malware and malicious freaks.

### X86-64
```shell
curl -fL https://github.com/JannikBulow/Bibble/releases/download/v0.1.0/bibble-0.1.0-1-x86_64.pkg.tar.zst -o /tmp/bibble.pkg.tar.zst && sudo pacman -U /tmp/bibble.pkg.tar.zst
```

### ARM
There is no official arm build. See [Build from source](#build-from-source)

### To uninstall
```shell
sudo pacman -R bibble
```

## MacOS
No.

## Build from source
Requires CMake, NASM and your favorite C++ compiler.

```shell
git clone https://github.com/JannikBulow/Bibble.git && cmake -S Bibble -B Bibble/build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local && cmake --build Bibble/build -j && sudo cmake --install Bibble/build
```

### To uninstall
There is no easy way to uninstall the project when built from source. You just have to delete the files yourself.\
If you really need help with this, please feel free to open an issue.