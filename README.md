# Flower-Kernel

GitHub Actions build for Xiaomi Qualcomm MSM8937 / MSM8917 family devices.

## Build configuration

- Workflow repository: `Rikk2012/Flower-Kernel`
- Workflow branch: `main`
- Kernel source: [LineageOS/android_kernel_xiaomi_msm8937](https://github.com/LineageOS/android_kernel_xiaomi_msm8937)
- **LineageOS kernel source branch: `lineage-19.1`**
- Defconfig: `lineageos_mi8937_defconfig`
- Architecture: ARM64
- KernelSU: [backslashxx/KernelSU](https://github.com/backslashxx/KernelSU), integrated with `kernel/setup.sh`
- Kernel local name: `flower-kernel-happy-new-year-edition`

The workflow repository remains on its existing `main` branch. The `lineage-19.1` branch is used only when cloning the LineageOS kernel source.

The upstream Mi8937 defconfig enables MSM8937 and MSM8917 platform support. This does not make every device interchangeable: matching device DTBs, vendor modules, boot image layout, and device-specific configuration are still required.

## Run

1. Open **Actions**.
2. Select **Build Flower Kernel**.
3. Choose **Run workflow** on `main`.
4. Download artifact `flower-kernel-happy-new-year-edition`.

The artifact contains `Image.gz`, available DTB/DTBO files, `kernel.config`, and build metadata.

## Safety and compatibility

This workflow builds kernel artifacts only; it does not package a device-specific `boot.img` or recovery ZIP. Do not flash the raw `Image.gz` directly. Verify the target device's exact kernel/DTB/boot-image requirements and retain a known-good boot image before testing.
