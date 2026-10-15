# Beginning
As I already [mentioned](https://github.com/MistWorks), main goal of this ecosystem is detailed learning of x86_64 PC working process. Because of that, all components of this system are written from scratch

At this point we have 3 projects:
- Mist (Kernel)
- Minit (Bootloader)
- Mistic (libc)

## Docs navigation
This documentation describes:
- [Architecture](ARCHITECTURE.md) of ecosystem
- [Contributing](CONTRIBUTING.md) guide
- [Roadmap](ROADMAP.md) of whole project
- [How to build and boot](BUILDnBOOT.md) guide

Every part of the ecosystem has (or will have) own, more detailed and specification-full documentation:
- [Mist](https://github.com/MistWorks/Mist/tree/main/docs) 
- [Minit](https://github.com/MistWorks/Minit/tree/main/docs) 
- [Mistic](https://github.com/MistWorks/Mistic/tree/main/docs)

## Status and limits
- Supported: x86_64 processor arch, Legacy BIOS mode, VGA text mode
- Not supported: UEFI, other architectures, other output types

## Fast start
If you don't want to learn all details and just want to try, make sure that you have:
- git
- clang
- QEMU
- NASM
- make
- ld
- dd

On your PC
Then do:

- Main directory:
``` shell
mkdir MistWorks && cd MistWorks
```

- Clone all repos:
```shell
git clone https://github.com/MistWorks/Mistic
git clone https://github.com/MistWorks/Minit
git clone https://github.com/MistWorks/Mist
```

- Make and boot:
```shell
cd Mist
make && make run
```

Mist will build and use its dependencies by itself
## Get help
- All GitHub issues are opened
  - [Issues](https://github.com/MistWorks/Mist/issues) for Mist
  - [Issues](https://github.com/MistWorks/Minit/issues) for Minit
  - [Issues](https://github.com/MistWorks/Mistic/issues) for Mistic
  - [Issues](https://github.com/MistWorks/Docs/issues) for entire ecosystem
- My [email](mailto:imdevyz@gmail.com)
- My [Telegram channel](https://t.me/DevyzLog) and [DM](https://t.me/ImDevyz)
- My Discord username: `imdevyz`

## License
All MistWorks projects use MIT License. So, you can do anything with the code, just don't forget to credit me