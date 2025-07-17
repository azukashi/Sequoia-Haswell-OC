# 🛠️ macOS Sequoia Haswell OpenCore

![Banner](https://socialify.git.ci/azukashi/Sequoia-Haswell-OC/image?custom_language=Apple&description=1&font=Jost&language=1&logo=https%3A%2F%2Fdortania.github.io%2FOpenCore-Legacy-Patcher%2Fhomepage.png&name=1&owner=1&pattern=Floating+Cogs&theme=Dark)

My daily driver Hackintosh configuration for Haswell (4th-Gen) of Intel Core running with H81 chipset.

## 📦 Configuration

| Specification | Details                                                                                   |
| ------------- | ----------------------------------------------------------------------------------------- |
| Motherboard   | KYO Kaizen H81-G573U[^3]                                                                  |
| Processor     | Intel Core i5-4570 @ 3.20 Ghz                                                             |
| Graphics      | NVIDIA GeForce GT 730 (Kepler)[^4]                                                        |
| Audio         | Realtek ALC662 (`alcid=5`)                                                                |
| Network       | Realtek Onboard Ethernet (no Wi-Fi card)                                                  |
| Boot-Args     | `-v keepsyms=1 debug=0x100 alcid=5 amfi_get_out_of_my_way=0x1 ipc_control_port_options=0` |
| SMBIOS        | iMac20,1 (Desktop with dGPU)[^2]                                                          |

> [!NOTE]
>
> -   `amfi_get_out_of_my_way=0x1` is a workaround to fix Haswell graphics using OCLP[^1].
> -   `ipc_control_port_options=0` is a workaround to fix crashing issue of some apps (Skype, WhatsApp, Spotify, etc.)

## 🔓 Disabling SIP (System Integrity Protection)

If you are using an incompatible graphic card (dropped support, etc.) you should disable SIP (System Integrity Protection) to patch your unsupported graphic card with OCLP (OpenCore-Legacy-Patcher)[^1]. This enables your system to fully use GPU acceleration feature.

1. Launch a terminal (iTerm2 or stock) and type these command

    ```sh
    $ sudo spctl --master-disable
    ```

2. Restart your PC, and enter recovery (dmg) image of your macOS drive
3. On the menu bar, choose Utility > Terminal and type these command
    ```sh
    $ csrutil disable
    $ csrutil authenticated-root disable
    ```
4. Restart and boot to your system.

## 🔧 Improvements

-   This version was initially prepared using OpenCore 1.0.0 for macOS Ventura (13.6.7).
-   This EFI config has been tested on macOS Sonoma and it was running well (14.7.5).
-   This EFI config has been tested on macOS Sequoia (15), but there are [known stability and cosmetics issues due to Legacy Metal Graphics Support](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/1008) on NVIDIA Kepler GPUs (I'm using an NVIDIA GT 730 with 1 GB of memory.)
-   This EFI config has not yet been tested with macOS Tahoe (26). I don't know if this version is still Hackintosh-able or if it still supports Intel-based systems. This version is still in the Developer Beta stage at the time of writing this text.

> [!NOTE]
> If you want to upgrading to latest macOS version such as Tahoe (26) or newer version, take a look at supported device models first and just change the SMBIOS on the `config.plist` with the supported SMBIOS value using GenSMBIOS tool and you are ready to upgrade.

## 🖼️ Screenshots

These are screenshots that I took on macOS Ventura (version 13.6.7).

![Image 1](https://ipfs.filebase.io/ipfs/QmSMoahrJTDkfvXFf24ikU4AB7TdZyghKY2vdPCkxdSSfA)
![Image 2](https://ipfs.filebase.io/ipfs/QmV45gHoGWBvf1AWpej2NAv5S5Ujv3Deu57iCCrZ3RtEz6)
![Image 3](https://ipfs.filebase.io/ipfs/Qmf96N3RBruPPyN6cKemkgbKWZGxKWMfqDcUB8HRcNTRPN)

[^1]: OCLP (OpenCore Legacy Patcher) is a Python-based project for both running and unlocking features in macOS on supported and unsupported Macs, such as Patching GPU drivers.
[^2]: For those using desktop with iGPU (Integrated GPU), they should use `iMac18,1` for their SMBIOS.
[^3]: Please note that VGA (D-SUB) onboard port wouldn't work. Only HDMI onboard that will work.
[^4]: Highest Supported OS for NVIDIA Kepler GPU series are macOS Big Sur (11). Further macOS version needs to be patched with OCLP.
