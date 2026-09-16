# MaanyaOS Confidential — coreboot Rebrand (PreBeta)

This is a fork of upstream [coreboot](https://coreboot.org) with OEM branding
applied for **MaanyaOS**. It is intended to be built and flashed/booted from
a custom Linux distro (e.g. via QEMU or on real hardware you control).

## What was changed

| Item | File | New value |
|---|---|---|
| Mainboard vendor (SMBIOS Type 1/2 "Manufacturer") | `src/mainboard/emulation/Kconfig` | `MaanyaOS` |
| Mainboard part number / model (SMBIOS "Product Name") | `src/mainboard/emulation/qemu-q35/Kconfig` | `MaanyaOS-Q35-PreBeta` |
| Firmware/coreboot version suffix (shown in boot log, `dmidecode -t bios`) | `src/Kconfig` (`LOCALVERSION` default) | `-MaanyaOS-PreBeta` |
| Ready-made build config | `configs/config.maanyaos_q35` | pre-fills the three values above |

These three Kconfig values are the canonical source for OEM identity in
coreboot — they flow automatically into:
- `src/lib/identity.c` (`mainboard_vendor`, `mainboard_part_number`, `mainboard_name`)
- `src/lib/version.c` / `src/lib/coreboot_table.c` (`coreboot_version`)
- SMBIOS/DMI tables (`src/arch/x86/smbios.c`), so `dmidecode -t 0` / `-t 1` /
  `-t 2` and the boot log will show `MaanyaOS`, `MaanyaOS-Q35-PreBeta`, and
  the `-MaanyaOS-PreBeta` version suffix.

## Building

```sh
# fetch build toolchain + submodules (first time only)
make crossgcc-i386 CPUS=$(nproc)
git submodule update --init --checkout

# use the pre-branded config
cp configs/config.maanyaos_q35 .config
make olddefconfig

# build
make -j$(nproc)
```

The resulting image is at `build/coreboot.rom`. Boot it under QEMU with:

```sh
qemu-system-x86_64 -M q35 -bios build/coreboot.rom -serial stdio
```

## Verifying the branding

From your custom Linux distro, once booted under this firmware:

```sh
sudo dmidecode -t bios -t system -t baseboard
```

You should see `MaanyaOS` as manufacturer and `MaanyaOS-Q35-PreBeta` as the
product/board name, with the coreboot version string ending in
`-MaanyaOS-PreBeta`.

## Notes before you push this to GitHub

- coreboot is licensed **GPL-2.0-only**. A public fork must keep `COPYING`
  and existing copyright headers intact — you're free to rebrand OEM
  identity strings (that's a normal, supported customization point) but not
  strip upstream authorship/license notices.
- "Confidential" in a public GitHub repo is contradictory — if this is meant
  to stay private, use a private repo instead of a public one.
- If you're targeting real hardware rather than QEMU, swap the mainboard
  target (`src/mainboard/<vendor>/<board>`) and adjust
  `configs/config.maanyaos_q35` accordingly — every physical board needs
  board-specific devicetree/GPIO config beyond just the branding strings.
