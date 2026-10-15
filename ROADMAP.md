# Roadmap
Every project in the ecosystem has its own roadmap, also as so does MistWorks

## Mist
### Done
- Compatibility with Minit to boot
- Physical Memory Manager (PMM)
- Virtual Memory Manager (VMM)
- Interrupt Descriptors Table (IDT)
- Programmable Interrupt Controller (PIC) driver
- Keyboard and VGA drivers
- Minimal shell

### In process
- Higher half mapping
_Focus were temporary switched to other projects_

### Planned
- PIT driver
- Multitasking
- Disk (AHCI) driver
- Third-party programs
- Ring 3 and userspace
- Syscalls


## Minit
### Done
- Fast A20 gate
- Loading kernel to memory from disk (hardcoded address and size)
- Common GDT setup
- Far jump to protected mode
- Common paging setup
- EFER.PAE and EFER.LME enable
- Far jump to long mode
- ELF64 parsing in second boot stage
- Loading kernel to wanted by it address
- Giving control to kernel

### In process
- Real-mode thunk
- FS supporting

### Planned
- Configuration file
- Compatibility with third-party kernels

## Mistic
### Done
- Memory module
- String module
- Integer math module
- Formatting module

### In process
- Standardized errors
- "Weak" panic function (watch [Mistic doc](https://github.com/MistWorks/Mistic/doc))
- Modules improvement
- Bug fixes

### Planned
- More modules
- Float math module
- Quality-of-life improvements

## MistWorks
### Done
- Compatibility between all ecosystem parts
- Working on real hardware
- What is done in each project

### In process
- Documentation for all projects
- Own FS (Simple, read-only)

### Planned
- Supporting FAT32/ext4
- Own C compiler (far future)