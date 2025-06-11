# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Kernel patches from pOOBs4 by @ChendoChap and ported for 7.00-9.60
  - 233 bytes to 307 bytes
- Payload loader from pOOBs4 by @ChendoChap
- `PROT_READ`, `PROT_WRITE`, `PROT_EXEC` constants for payload loader by
  @janisslsm
- Added loading payload from file
- Added read8/read16/write8/write16 functions
- Added 7.00-9.60 support
  - Initial 9.00-9.60 ROP chain, by @janisslsm
- Added GitHub actions to build PRs, push to `main`, and tags for releases.

### Fixed

- Fixed corrupt pointer cleanup by abc
- Fixed `ip6po_rthdr` offset for PS5 by abc
- Verified the number of blocking requests needed to be two by abc
- Only run kernel exploit once by checking setuid by @JTAG7371
- ~~Restore syscall 661 (`sys_aio_submit()`) after patching by @janisslsm~~
  - Was not actually restoring syscall. Used a different method/rewrote to
  restore in kpatch. (Shellcode change 4)
    - Shellcode from 345 bytes to 444 bytes

### Changed

- Cleanup/Linting/Tweaks/Fixes/etc
  - Default Prettier config w/ 999 line length
  - Default eslint config "problems" list trimmed down
- Reorder make_aliased_pktopts to try and reclaim memory earlier, by abc
- Simplify shellcode a little bit more
  - No external headers
  - Added `-fcf-protection=none` flag to skip added "endbr64" instructions
  (Shellcode change 1)
    - 307 bytes to 295 bytes
  - Changed `restore` and `do_patch` to be inlined (Shellcode change 2)
    - 307 bytes to 282 bytes
  - Changed to `-03` for execution speed optimization (Shellcode change 3)
    - 282 bytes to 345 bytes
  - Move kbase calc to main function (Shellcode change 5)
    - 444 bytes to 418 bytes

## [1.5.1] - 2025-05-12

### Added

- `.gitignore` for kpatch output
- Auto detect console type and firmware in `config.mjs`
  - Used elsewhere to determine which offsets/patches/ROP chain are used
- **WIP:** Add 8.50-9.60 support
  - All offsets found
  - Running into some issue here. Wiped out my JOP chains to redo them...

### Fixed

- Call `lapse.mjs` rather than `code.mjs`
- Makefile for kpatch builds all currently available

### Changed

- Use relative locations rather than absolute
- Changed kpatch binaries to just be shellcode vs full ELFs
  - 5,216 bytes to 257 bytes.
- Build kpatch binaries with `-Os` rather than `-O`
  - 257 bytes to 233 bytes.
- Renamed/Formatted `CHANGELOG.md`, `README.md`, and `LICENSE`

## [1.5.0] - 2025-05-08

### Added

- Lapse kernel exploit

### Fixed

- Rewrite PSFree exploit

## [1.4.0](#) - 2024-01-25

### Added

- Kernel patch payload for 8.0x

### Fixed

- Remove the risk of crashing from using the Chain classes
- Remove the risk of crashing from using `make_buffer()`
- (PS5 < 3.00) use valid config at `exploit.mjs:setup_ssv_data`

## [1.3.0](#) - ????-??-??

### Added

- ROP chain managers for 8.5x, 9.0x, 9.5x

### Fixed

- Improve the speed and reliability of the exploit (`exploit.mjs`)

### Removed

- Support for webkitgtk 2.34.4, see 1.0.0 for a working implementation

## [1.2.0](#) - 2023-12-03

## Added

- Support for PS4 6.00-6.20

## [1.1.0](#) - ????-??-??

### Added

- Support for running ROP chains (PS4 8.03)
- Support for calling syscalls (PS4 8.03)

## [1.0.0](#) - ????-??-??

### Added

- Proof-of-concept code to gain arbitrary read/write (PS4 6.50-9.60/PS5 1.00-5.50)

[unreleased]: https://github.com/Al-Azif/psfree-lapse/compare/v1.5.1...HEAD
[1.5.1]: https://github.com/Al-Azif/psfree-lapse/compare/v1.5.0...v1.5.1
[1.5.0]: https://github.com/Al-Azif/psfree-lapse/releases/tag/v1.5.0
