# Flower-Kernel

GitHub Actions build for the Xiaomi Mi8937 device family.

## Build configuration

- Workflow repository branch: `main`
- Kernel source: [LineageOS/android_kernel_xiaomi_msm8937](https://github.com/LineageOS/android_kernel_xiaomi_msm8937)
- Kernel source branch: `lineage-19.1`
- Kernel version: Linux 4.9.337 (from the selected source branch)
- Defconfig: `lineageos_mi8937_defconfig`
- Architecture: ARM64
- Kernel local name: `flower-kernel-happy-new-year-edition`
- Two build variants: KernelSU and No-KSU
- Installer: AnyKernel3, containing `Image.gz-dtb`

## Device-family scope

The source defconfig enables these Xiaomi board configurations:

- `LAND` — Redmi 3S family
- `ROVA` — Redmi 4A / Redmi 5A unified board (standard/non-Oreo Riva DTB selection)
- `SANTONI` — Redmi 4X
- `ULYSSE` — Redmi Note 5A family

The AnyKernel device-check aliases are: `rolex`, `riva`, `rova`, `land`, `santoni`, `ugglite`, and `ugg`.

**Important limitations:** `prada` is intentionally not listed because this LineageOS source's Xiaomi Kconfig has no Prada board option/DTB selection. The separate `MACH_XIAOMI_RIVA_OREO` option is not enabled because the source Kconfig documents that it removes Redmi 4A support; therefore this unified build must not be assumed compatible with the Riva Oreo-bootloader variant. Device aliases in AnyKernel only gate the installer; they do not prove hardware compatibility.

## KernelSU variant

The KSU build uses backslashxx/KernelSU and enables the options supported by its Kconfig:
- `CONFIG_KSU=y`
- `CONFIG_KSU_TAMPER_SYSCALL_TABLE=y`
- `CONFIG_KSU_LSM_SECURITY_HOOKS=y`
- `CONFIG_KSU_FEATURE_ADBROOT=y`

The No-KSU build does not integrate KernelSU.

Both variants enable embedded kernel config (`IKCONFIG` and `IKCONFIG_PROC`) and build `Image.gz-dtb` plus the configured device trees.

## Run

1. Open **Actions**.
2. Select **Build Flower Kernel (Mi8937 Unified)**.
3. Run the workflow on `main`.
4. Download the corresponding `Flower-Kernel-Mi8937-KSU` or `Flower-Kernel-Mi8937-No-KSU` artifact.

Each artifact includes an AnyKernel ZIP, the effective `.config`, and build metadata. The ZIP contains an empty root-level file named `banner`, ready for your own text.

## Compatibility and testing

A successful compile or a matching AnyKernel device alias does not guarantee that a kernel will boot on every ROM or bootloader. The build has not been boot-tested across the listed devices. Keep a device-matched stock boot image available and verify the exact bootloader/DTB/vendor-module combination before any test.
