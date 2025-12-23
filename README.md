# BBR to Raspberry Pi

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/fisherred/BBR-to-Raspberry-Pi/build.yml?label=Build%20Kernel&logo=github)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/fisherred/BBR-to-Raspberry-Pi)

**Automated BBRv3 Kernel Builder for Raspberry Pi**

This project automatically builds a custom Linux Kernel for Raspberry Pi that combines:

1.  **Official Raspberry Pi Source**: Ensures full hardware support (WiFi, Bluetooth, GPIO, VideoCore).
2.  **Google BBRv3 TCP Stack**: Adds the latest congestion control algorithm for improved network throughput and lower latency.
3.  **Your Custom Config**: Uses a configuration extracted from a working Pi to minimize bloat and maximize compatibility.

## 🚀 How It Works

This repository uses **GitHub Actions** to perform a daily automated build:

1.  Clones the latest `rpi-6.13.y` kernel source from the Raspberry Pi Engineering team.
2.  Merges the `v3` branch from Google's BBR repository.
3.  Applies the `pi.config` (hardware configuration).
4.  Cross-compiles the kernel for ARM64.
5.  **Releases** the result as installable `.deb` packages in the [Releases](https://github.com/fisherred/BBR-to-Raspberry-Pi/releases) section.

## 📦 Installation

No need to build anything yourself! Just download the latest release.

1.  Go to the [Releases Page](https://github.com/fisherred/BBR-to-Raspberry-Pi/releases).
2.  Download the 3 `.deb` files:
    - `linux-image-...deb`
    - `linux-headers-...deb`
    - `linux-libc-dev-...deb`
3.  Transfer them to your Raspberry Pi.
4.  Install:
    ```bash
    sudo dpkg -i linux-*.deb
    ```
5.  Reboot:
    ```bash
    sudo reboot
    ```
6.  Verify BBRv3 is running:
    ```bash
    uname -r
    # Should see "bbrv3" in the name
    sysctl net.ipv4.tcp_congestion_control
    # Should return "bbr"
    ```

## 🛠 Manual Build (Docker)

If you prefer to build it yourself locally on a Mac or Linux machine:

1.  Run the auto-builder script:
    ```bash
    ./auto_update_hybrid.sh "your_pi_password"
    ```
    This will SSH into your Pi to get the config, build the kernel in Docker, and deploy it back to the Pi automatically.

## 📝 Configuration

The `pi.config` file in this repository is the kernel configuration used for the build. It was extracted from a working Raspberry Pi 4/5 environment.

## ⚖️ License

Dual BSD/GPL (Inherited from Linux Kernel).
