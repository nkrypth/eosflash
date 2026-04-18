# Changelog

### v1.3
- `flash` - general improvements and better validation for number of corner cases
- **Bugfix** - fixed incorrect OS copy offset when building a 4 MB ROM (now `0x20000`, was `0x10000`).
- **Bugfix** - fixed issue where 128 KB bootloader with `--2mb`was silently truncated to 64 KB.

### v1.2
- **Experimental** - `verify` now shows bootloader version banner when inspecting bootloader-only binary
- `flash` - now accepts up to two binaries of any type as long they will produce correct output. `--btl` is now exclusively an output.

### v1.1
- **Windows** - Hardened floppy read/write reliability: fixed `ERROR_UNRECOGNIZED_MEDIA` on verify,

### v1.0 - initial release
