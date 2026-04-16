# eosflash

Cross-platform CLI for inspecting, transforming, and writing E-MU E4 / EIV / E-Synth sampler firmware (EOS). Classic and Ultra generations.
Runs natively on Linux and modern Windows. Supports raw disks, legacy E-MU DOS executables, and full and partial ROMs.

> **Note:** Use [emu.tools](https://emu.tools) to update E4 samplers via MIDI — no floppies required!

---

## Usage

### Inspect a file or floppy disk

```bash
eosflash verify eos.img                # Verify RAW disk image
sudo eosflash verify /dev/fd0          # (Linux)   physical floppy — requires sudo
eosflash verify a:                     # (Windows) physical floppy
```

### Compare two sources

```bash
eosflash verify a.eos b.eos            # compare payloads of two OS binaries
sudo eosflash verify eos.img /dev/fd0  # (Linux)   RAW image vs physical floppy
eosflash verify eos.exe a:             # (Windows) DOS executable vs physical floppy
```

### Export between formats

```bash
eosflash export os.exe --img out.img --eos out.eos  # DOS executable -> RAW image, OS binary
```

### Write floppy disk(s)

Works with both OS and Flash Prep sources.

```bash
sudo eosflash write os.eos --drv /dev/fd0     # (Linux)   create OS disk
eosflash write os.img flashprep.img --drv a:  # (Windows) OS and Flash Prep
```

---

## Advanced ROM manipulation

The `flash` command splits, combines, compresses and decompresses ROM binaries.

```bash
# Combine / split IC dumps
eosflash flash low.bin high.bin --rom full.rom       # combine two IC halves -> ROM
eosflash flash full.rom --lo low.bin --hi high.bin   # split ROM -> two hi/lo halves

# Extract / reassemble payloads
eosflash flash full.rom --eos os.eos --btl boot.btl  # extract OS + bootloader
eosflash flash os.eos --btl boot.btl --rom full.rom  # reassemble OS + bootloader -> ROM

# Compress / decompress
eosflash flash compressed.eos --eos out.eos --4mb    # decompress 2MB -> 4MB compatible
eosflash flash uncompressed.eos --eos out.eos --2mb  # compress to fit in 2MB target
```

### What to avoid

- **Don't flash Ultra OS onto a Classic** - Classic (1st/2nd gen EIV/E4) uses Motorola 68020; E4 Ultra uses Coldfire MCF5206E. They are not compatible.
- **Don't write a corrupted source** - It won't boot on real hardware. Use `--force` only to investigate corrupted files.
- **Don't use a 64KB bootloader with a 4MB ROM target** - The 4MB FlashROM has a different RAM map and IC layout; a 64 KB bootloader will not boot.

---

## Bugs / support

Floppy drive issues (bad sectors, mechanical failures) are normal, use freshly formatted disks before writing OS.

For everything else: open an issue here on GitHub or ping **@nkrypth** on the Madlabz Discord: [madlabz.info](https://madlabz.info)
