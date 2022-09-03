# Wrapper for mpdecimal

## For users

When installing through nimble, configuration is done automatically.

## For development on your local machine

mpdecimal checks at compile-time if the computer is 32-bit or 64-bit and GCC builtin __uint128_t.
It then generates `mpdecimal.h` from the template `mpdecimal.h.in`.

To support multiple architectures: x86_64, ARMv7 32-bit and ARMv9 64-bit you should run the
`genSources.sh` build script which would configure mpdecimal properly for your platform.

## Details

When doing ./configure, mpdecimal creates:
  - Makefile (unused)
  - libmpdec/Makefile (unused)
  - tests/Makefile (unused)
  - limpdec/mpdecimal.h (used everywhere)
  - config.h (contains global defines like pointer size and uint128 support)

For our Nim wrapping purpose:

1. We copy the source files in a temp dir `mpdecimal_temp`
2. We run .configure in this dir
3. We copy `config.h` to a `generated`destination folder
4. We append `#include "config.h"` and copy the `.h` and `.c` files to the `generated` destination folder
5. We delete `mpdecimal_temp`
