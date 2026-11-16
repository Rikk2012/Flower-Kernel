# Flower-Kernel

Kernel build automation for **Xiaomi Redmi 5A (riva)**, based on the unified
LineageOS MSM8937 kernel source.

## Build target

- Source: [LineageOS/android_kernel_xiaomi_msm8937](https://github.com/LineageOS/android_kernel_xiaomi_msm8937)
- Branch: \`lineage-19.1\`
- Kernel base reported by the source Makefile: Linux **4.9.337**
- Defconfig: \`lineageos_mi8937_defconfig\`
- Architecture: ARM64
- KernelSU: integrated using [backslashxx/KernelSU](https://github.com/backslashxx/KernelSU)
  and its \`kernel/setup.sh\` script; the script checks out the latest available tag.
- Build options: \`CONFIG_KSU=y\`, \`CONFIG_KPROBES=y\`, \`CONFIG_KALLSYMS=y\`,
  and \`CONFIG_KALLSYMS_ALL=y\`.

The existing kernel source, defconfig, and local version naming are retained.

## Run a build

1. Open the **Actions** tab in this repository.
2. Select **Build Flower Kernel**.
3. Press **Run workflow** and confirm the \`main\` branch.
4. When the run completes, open the run and download the artifact
   \`Flower-Kernel-riva-lineage-19.1\`.

The artifact contains \`Image.gz\`, compiled device-tree blobs (when produced),
the final kernel config, and build information including the KernelSU revision.

## Important

This workflow currently produces kernel build artifacts, **not a flashable
boot.img or recovery ZIP**. Do not flash the raw \`Image.gz\` directly from
recovery. A device-specific packaging step and testing on the Redmi 5A are
still required. KernelSU integration compiling successfully does not by itself
prove that all KernelSU features work at runtime or that the kernel is safe to
flash. Keep a backup of the stock boot image before testing.
