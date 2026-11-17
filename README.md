# Flower Kernel

GitHub Actions build for the Xiaomi Mi8937 unified device family, using the official MiThorium Linux 4.9.337 manifest.

## Build configuration

- Kernel local name: `Flower-Kernel`
- Kernel source: [Mi-Thorium/kernel_msm-4.9](https://github.com/Mi-Thorium/kernel_msm-4.9)
- Source branch: `mithorium/a14/master`
- Kernel version: Linux 4.9.337
- Defconfig: `vendor/msm8937-perf_defconfig` plus MiThorium Android and Xiaomi MSM8917/MSM8937 fragments
- Architecture: ARM64
- Cross compiler: GCC 13.3.0
- Kernel image: `Image.gz-dtb`
- Installer: AnyKernel3, pinned to `6f88dff82b786e879b255a8e1523547c4f62d031`
- Boot layout: non-A/B `boot`, using AnyKernel3 `dump_boot` / `write_boot`

## MiThorium manifest dependencies

The workflow clones all projects declared by the official `mithorium-4.9` manifest, including both MSM8937 and SDM439 DTS/techpack repositories. The SDM439 techpack is required because the shared `techpack/Kconfig` sources `techpack/xiaomi-sdm439/Kconfig` even when building `msm8937_defconfig`.

## Device scope

The uploaded banner is included byte-for-byte in each installer. Device trees built and appended are:

- `land` — Redmi 3S / 3X
- `riva` — Redmi 5A
- `santoni` — Redmi 4X
- `ugg` — Redmi Note 5A / Y1 Prime
- `ugglite` — Redmi Note 5A / Y1 Lite
- `rolex` — Redmi 4A
- `prada` — Redmi 4 Standard

## Variants and hooks

- `KSU` — backslashxx KernelSU v3.3.1, with syscall-table and LSM security hooks, ADB root, and in-tree build detection.
- `No-KSU` — no KernelSU integration; keeps `CONFIG_KPROBES`, `CONFIG_KALLSYMS`, and `CONFIG_KALLSYMS_ALL` enabled for patcher compatibility.

The KSU variant enables `CONFIG_KPROBES`, `CONFIG_KSU_TAMPER_SYSCALL_TABLE`, and `CONFIG_KSU_LSM_SECURITY_HOOKS`. It disables `CONFIG_KSU_HACK_ARM64_BRANCH_LINK`, which the KernelSU Kconfig recommends for newer kernels (4.19+), not this Linux 4.9 tree.

A CPU/GPU overclock variant is intentionally not emitted yet. The Redmi 5A (`riva`) uses the MSM8917 device-tree path; an OC variant requires a device-validated CPU/GPU OPP and voltage/thermal patch. No Yoru archive has been supplied or could be retrieved from the Telegram group, so unverified clock/voltage values will not be added.

## Build

1. Open **Actions**.
2. Select **Build Flower Kernel (MiThorium Mi8937 Unified)**.
3. Run the workflow on `main`.
4. Download the `Flower-Kernel-Mi8937-KSU` or `Flower-Kernel-Mi8937-No-KSU` artifact. These are the two currently implemented variants; an OC variant remains blocked pending a validated patch.

Each artifact contains the AnyKernel ZIP, effective kernel config, and build metadata. The installer contains the supplied non-empty `banner` file.

## Validation

The workflow checks the kernel version, required board configs, `CONFIG_KPROBES`, KSU hook selections, all seven DTB outputs, appended DTB payload/order, and banner bytes in the ZIP. A successful compile is not a boot test; the package must still be tested on the target ROM/device before it can be called boot-verified.
