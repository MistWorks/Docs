# Contributing

MistWorks is fully open-source and open to contributions. Bug reports, fixes, and new features are welcome. See [roadmap](ROADMAP) for what is planned and what is in progress

## Before you start
Open an Issue in the repository you want to contribute to before sending a PR. Describe the feature or bug. This saves time for everyone

## Don't
- Send untested PRs. At minimum, boot it in QEMU
- Use host libc (`glibc` or anything else) instead of Mistic
- Break compatibility between projects

## Code style
### Formatting
1. Tabs for indentation
2. `{` on the same line as the function name
3. For `if` and loops: either `{\n\n}` or a single line if the body is short

### Naming
1. Macros - `CAPS_LOCK` with `_` between words
2. Functions - short names, no special symbols

### Comments
1. English only
2. Content and style - up to you

### Headers
1. In `.h` files: first `#include "types.h"`, then `#include "FILENAME.h"`, then everything else
2. All includes have to be in header. `.c` file must include only own `.h`
3. In headers: `#pragma once` first (**not** include guards), then the content

### Types
Use only types from `types.h`. Do not include `stdio.h`

### Forbidden
1. Host libc dependency
2. `-O0`-specific hacks
3. Floating point in kernel code

### Example
`file.h`:
```c
#include "types.h"
#include "screen.h"

void ravefunc(int x);
```

`file.c`:
```c
#include "file.h"

#define EXAMPLE_MACROS(x, y) ((x) + (y))

void ravefunc(int x) {
	int z = 0;
	if (x <= 0) return;
	for (int i = 10; i > 0; i--) {
		z += EXAMPLE_MACROS(x, i);
	}
	print_num(z);
}
```

## Architecture rules
### Project boundaries
Each project has its own scope, and PRs must follow it:
- **Mist** - drivers, kernel, utilities
- **Minit** - boot process
- **Mistic** - hardware-independent code that doesn't depend on other MistWorks projects (except `sys/`, see [Mistic docs](https://github.com/MistWorks/Mistic/tree/main/docs))

### Compatibility
Although Mistic is a standalone libc, its functions must match glibc's behavior. Keep your code predictable

## Testing
There is no CI yet. Test manually:
1. [Build](BUILDnBOOT#Building) must pass without errors
2. [Boot](BUILDnBOOT#Booting%20in%20QEMU) in QEMU must pass without errors
3. If your change affects hardware, [test on real hardware](BUILDnBOOT#Booting%20on%20real%20hardware)

## Commits
1. Name commits so they describe the change
2. Reference the Issue you opened

## License
All MistWorks projects use the MIT License. By contributing, you agree that your contribution is licensed under MIT. Do not copy GPL-licensed code

## Communication
- All GitHub issues are opened
  - [Issues](https://github.com/MistWorks/Mist/issues) for Mist
  - [Issues](https://github.com/MistWorks/Minit/issues) for Minit
  - [Issues](https://github.com/MistWorks/Mistic/issues) for Mistic
  - [Issues](https://github.com/MistWorks/Docs/issues) for the ecosystem
- [Email](mailto:imdevyz@gmail.com)
- [Telegram channel](https://t.me/DevyzLog) and [DM](https://t.me/ImDevyz)
- Discord: `imdevyz`