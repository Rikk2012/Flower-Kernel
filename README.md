# Flower-Kernel

GitHub Actions build for the Xiaomi Mi8937 unified device family, using the official MiThorium Linux 4.9.337 source manifest.

## Build configuration

- Kernel source: [Mi-Thorium/kernel_msm-4.9](https://github.com/Mi-Thorium/kernel_msm-4.9)
- Source branch: `mithorium/a14/master`
- Kernel version: Linux 4.9.337
- Defconfig: `msm8937_defconfig` plus MiThorium Xiaomi MSM8937 fragments
- Architecture: ARM64
- Cross compiler: GCC 13.3.0 (matching the Yoru reference toolchain)
- Kernel image: `Image.gz-dtb`
- Installer: AnyKernel3, pinned to `6f88dff82b786e879b255a8e1523547c4f62d031`
- Boot layout: non-A/B `boot`, using AnyKernel3 `dump_boot` / `write_boot`

## Device scope

The uploaded banner is included verbatim in each installer. Device trees built and appended are:

- `land` — Redmi 3S / 3X
- `prada` — Redmi 4 Standard
- `riva` — Redmi 5A
- `rolex` — Redmi 4A
- `santoni` — Redmi 4X
- `ugg` — Redmi Note 5A / Y1 Prime
- `ugglite` — Redmi Note 5A / Y1 Lite

AnyKernel aliases additionally include `rova` for the Riva board naming used by ROMs. Aliases only gate installation; they do not guarantee compatibility with every ROM or bootloader.

## Variants

The workflow currently builds:
- `KSU` — backslashxx KernelSU with syscall-table tampering, LSM security hooks, ADB root, and in-tree build detection.
- `No-KSU` — no KernelSU integration.

The Yoru reference's `CONFIG_KSU_FEATURE_SULOG` is not present in the current backslashxx KernelSU Kconfig, so the workflow does not force an unknown option. A separate CPU+GPU overclock build is not advertised until a verified Mi8937-specific overclock patch is available; the Yoru reference's packaging/config details do not provide validated OC tables for this MiThorium source.

## Build

1. Open **Actions**.
2. Select **Build Flower Kernel (Mi8937 Unified)**.
3. Run the workflow on `main`.
4. Download the `Flower-Kernel-Mi8937-KSU` or `Flower-Kernel-Mi8937-No-KSU` artifact.

Each artifact contains the AnyKernel ZIP, effective kernel config, and build metadata. The installer contains the supplied non-empty `banner` file.

## Validation

The workflow checks the kernel version, required board configs, all seven DTB outputs, the appended DTB payload/order, and the banner bytes in the ZIP. A successful compile is not a boot test; the package has not been boot-tested across all listed devices.
