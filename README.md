# Flower-Kernel

Kernel build automation for **Xiaomi Redmi 5A (riva)**, based on the unified
LineageOS MSM8937 kernel source.

## Build target

- Source: [LineageOS/android_kernel_xiaomi_msm8937](https://github.com/LineageOS/android_kernel_xiaomi_msm8937)
- Branch: `lineage-19.1`
- Kernel base reported by the source Makefile: Linux **4.9.337**
- Defconfig: `lineageos_mi8937_defconfig`
- Architecture: ARM64
- Required kernel options are enabled during CI: `KPROBES`, `KALLSYMS`, and `KALLSYMS_ALL`.

## Run a build

1. Open the **Actions** tab in this repository.
2. Select **Build Flower Kernel**.
3. Press **Run workflow** and confirm the `main` branch.
4. When the run completes, open the run and download the artifact
   `Flower-Kernel-riva-lineage-19.1`.

The artifact contains `Image.gz`, compiled device-tree blobs (when produced),
the final kernel config, and build information.

## Important

This workflow currently produces kernel build artifacts, **not a flashable
boot.img or recovery ZIP**. Do not flash the raw `Image.gz` directly from
recovery. A device-specific packaging step and testing on the Redmi 5A are
still required.

APatch compatibility is not claimed as complete merely because the required
symbol/probe options are enabled; APatch/KernelPatch integration and boot-image
packaging must be validated separately before distributing a flashable build.
