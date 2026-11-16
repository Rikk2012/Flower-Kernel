# Flower-Kernel

GitHub Actions build setup for the unified Xiaomi Qualcomm **MSM8937 / MSM8917** kernel family.

## Build configuration

- Build repository: `Rikk2012/Flower-Kernel`
- Workflow branch: `lineage-19.1`
- Kernel source: [LineageOS/android_kernel_xiaomi_msm8937](https://github.com/LineageOS/android_kernel_xiaomi_msm8937)
- Kernel source branch: `lineage-19.1`
- Kernel version in that source branch: Linux `4.9.337`
- Architecture: `arm64`
- Defconfig: `lineageos_mi8937_defconfig`
- SoC configuration: enables both `CONFIG_ARCH_MSM8937` and `CONFIG_ARCH_MSM8917`
- KernelSU: [backslashxx/KernelSU](https://github.com/backslashxx/KernelSU), integrated with its `kernel/setup.sh` script.

The unified Mi8937 defconfig is used because the LineageOS source contains both MSM8937 and MSM8917 platform support. This is a shared platform kernel build, not a guarantee that one output is interchangeable across every device: each device still needs matching DTBs, device configuration, vendor modules, and boot-image packaging.

## Run the build

1. Open the repository's **Actions** tab.
2. Select **Build Flower Kernel**.
3. Choose **Run workflow** on branch `lineage-19.1`.
4. Download the artifact named `Flower-Kernel-MSM8937-MSM8917-lineage-19.1`.

The artifact contains `Image.gz`, available DTB/DTBO outputs, the final kernel config, and build metadata including the exact kernel and KernelSU commits.

## Important

This workflow produces kernel build artifacts only. It does **not** create a device-specific flashable `boot.img` or recovery ZIP. Do not flash `Image.gz` directly. Device-specific boot-image packaging and testing are separate steps; preserve a known-good boot image before any device testing.
