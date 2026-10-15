# How to Build and Boot
The way you just want to try it on QEMU is easier than if you want to test it on real hardware

## Prerequisites
Make sure you have these tools installed:

| Tools   | Why                                                                    |
| ------- | ---------------------------------------------------------------------- |
| `git`   | To get project sources or contribute                                   |
| `make`  | To build system                                                        |
| `clang` | To compile most parts of projects (excluding that was written in NASM) |
| `nasm`  | To compile remaining parts                                             |
| `ld`    | Linker                                                                 |
| `dd`    | To make an `.img` file or put it on your flash drive                   |
| `QEMU`  | To boot system                                                         |

## Getting sources
Mist requires Minit and Mistic, Minit requires Mistic ([why?](ARCHITECTURE)). So to try Mist you have to get the sources of all of them

Mistic and Minit directories **must** be in `../Mistic` and `../Minit` relative to the `Mist/` directory. I recommend to put each in `MistWorks/` directory just to not clog your file tree:
``` shell
mkdir MistWorks
cd MistWorks
```

Then clone sources with `git`:
``` shell
git clone https://github.com/MistWorks/Mist
git clone https://github.com/MistWorks/Minit
git clone https://github.com/MistWorks/Mistic
```

## Building
Mist's Makefile is set up so that is builds and Minit and Mistic by itself, so you only need to build Mist:
``` shell
cd Mist
make
```
The output will appear in `mbin/Mist.img`

But if you want to build Minit or Mistic separately, you can do it the same way with Mist:
```shell
cd Minit
make
```
It will also build and use Mistic by itself. The binary file will be in `build/Minit.img`

For Mistic:
```shell
cd Mistic
make
```
Currently, it has no any dependencies. Output will be in `build/mistic.a`

## Booting in QEMU
There is literally nothing difficult. Just do:
```shell
make run
```
In the `Mist/` directory after building. If you have all [prerequisites](#Prerequisites), QEMU will start without any errors. If there are any errors, you can report them [here](README#Get%20help)

If you want to use GDB for debug, use
```shell
qemu-system-x86_64 -drive format=raw,file=mbin/Mist.img -no-reboot -s -S
```
Instead. Then open new terminal window, open `Mist/` directory and execute:
```shell
make debug
```

## Booting on real hardware
**WARNING**: Try it *only* with flash drive, data on which you don't need. The instructions below will wipe all data from the target drive sectors

If you know what you are doing, make sure you are in `Mist/` directory and follow these instructions:
1. Plug in your flash drive and find its device name:
```shell
lsblk
```
You'll get output like (pseudo output):
```shell
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 238,5G  0 disk 
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0   732M  0 part /boot
└─sda3   8:3    0 237,3G  0 part 
sdb      8:16   0 931,5G  0 disk 
└─sdb1   8:17   0 931,5G  0 part /mnt/data
nvme0n1 259:0   0 476,9G  0 disk 
├─nvme0n1p1 259:1 0   512M  0 part /boot/efi
└─nvme0n1p2 259:2 0 476,4G  0 part /
```
In next commands examples I'll use `sdb` disk name. Please, be careful with disk names and use only that disk name that you want to use
2. Wipe the amount of space, the system will need, using `dd`:
```shell
sudo dd if=/dev/zero of=/dev/sdb bs=512 count=128
```
  - `if=/dev/zero` means that selected amount of sectors will be fully wiped
  - `of=/dev/sdb` is a disk that we are cleaning. *Use your disk name instead of `sdb`*
  - `bs=512` means block (sector) size equal 512 bytes
  - `count=128` means we are wiping 128 sectors, each 512 bytes (64KB at all)
  - It's needed to clean trash in needed sectors
3. Write `Mist.img` to the wiped area:
``` shell
sudo dd if=mbin/Mist.img of=/dev/sdb bs=512 count=128 conv=notrunc
```
`/dev/sdb` is *all* disk, not the partition, like `/dev/sdb1`
4. Plug in this flash drive in thetarget machine and turn it on
5. Before system started, enter system firmware (UEFI/BIOS)
6. Set boot priority to your flash drive
7. Enable CSM/Legacy BIOS mode in your firmware
8. Exit firmware and wait
9. If Mist boots without problems - you're done! 
## Troubleshooting
If you get an error, you can [get help](README#Get%20help)