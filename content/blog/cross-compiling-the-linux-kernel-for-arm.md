+++
title = "Cross-compiling the Linux kernel for ARM"
date = "2025-02-26"
description = "A simple guide to cross-compiling the Linux kernel for ARM, from setup to testing with QEMU."

[taxonomies]
tags = ["guide"]
+++

Seems fun, right? I didn't know anything related to this or what I was doing. I started by simply googling, you guessed it, `how to cross-compile the Linux kernel for ARM`, and that provided more than enough resources to get me started.

It also felt like a great way to get acquainted with the tools and concepts I might need later when working on embedded systems.

### Beginning

I went to [kernel.org](https://www.kernel.org/) and downloaded the latest version at the time, which was `6.13.2`, then extracted it using the command below:

```sh
 tar -xf linux-6.13.2.tar.xz
```

Moving into the new directory, I was greeted with a myriad of files, most of which I didn't know how to interpret.

### Figuring Things Out

This took me much longer than necessary because I initially used the wrong toolchain. More on that later.

At this point, I installed the necessary toolchains and other dependencies from AUR:

```sh
sudo pacman -S aarch64-linux-gnu-gcc
```

### Compiling

From what I learned, the kernel build process can be customized in many ways using the command below:

```sh
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig
```

After saving and exiting the config file, I proceeded straight to compiling with the following command:

```sh
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
```

Everything seemed fine, but the compilation was taking too long. After some research, I realized that adding `-jn`, such as `-j4` or `-j8`, would allow the compiler to use multiple threads, significantly speeding up the process.

```sh
make -j8 ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu-
```

### Testing

I was happy to have successfully compiled the kernel, but now I needed to test it. How? I chose to use QEMU to run the compiled kernel.

Initially, when I tried running it, nothing happened—no output, no errors, just a blank screen. After much fiddling and research, I discovered that I had installed and used the wrong toolchain. After switching to the correct toolchain, I was able to test the kernel, and it finally displayed errors. This was expected and confirmed that the compilation was actually successful.

```sh
qemu-system-aarch64 \
    -machine virt \
    -cpu cortex-a57 \
    -nographic \
    -smp 2 \
    -m 2048 \
    -kernel arch/arm64/boot/Image \
    -append "root=/dev/vda console=ttyAMA0"
```

Overall, this experience gave me a glimpse into what is involved in compiling and working with systems.