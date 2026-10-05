# buildX3_kernel

Kernel source for X3 (sharkl5pro / UMS512), Linux 4.14.193, Android 14 —
with KernelSU integrated (`kernel_x3/KernelSU/`).

Kernel is GPLv2; vendor-derived code and blobs remain property of their owners.

## Build

```sh
export PATH=<clang-r383902b>/bin:$PATH
cd kernel_x3
make O=out ARCH=arm64 CC=clang CLANG_TRIPLE=aarch64-linux-gnu- \
     CROSS_COMPILE=<aarch64-linux-android-4.9>/bin/aarch64-linux-android- bootimage
```

Build trees (`kernel_x3/out*`) are not tracked.
