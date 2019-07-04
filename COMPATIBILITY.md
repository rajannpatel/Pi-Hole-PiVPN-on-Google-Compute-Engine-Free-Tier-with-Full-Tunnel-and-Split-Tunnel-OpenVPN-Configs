# Supported & Compatible Devices & OSes

If you succeed or fail at implementing this OpenVPN solution on your device, please submit a Pull Request to this Repository with an update to the table below.

The tests columns refer to steps outlined under [Verify Everything Works](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs#verify-everything-works) in the **README.md** file.

## Phones

### Split Tunnel VPN

| make | model | os version | vpn app | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------- | -------------------- |
| Google | Pixel 3/3XL | Android 9 build# PQ3A.190605.003 | OpenVPN for Android 0.7.8 | Passed by @rajannpatel | Passed by @rajannpatel |
| ? | ? | Android 6.0.1 | OpenVPN for Android (version?) | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/40) by @Fliu777 | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/40) by @Fliu777 |

### Full Tunnel VPN

| make | model | os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| Google | Pixel 3/3XL | Android 9 build# PQ3A.190605.003 | OpenVPN Connect 3.0.5 | Passed by @rajannpatel | Passed by @rajannpatel | Passed by @rajannpatel |

## Tablets

### Split Tunnel VPN

| make | model | os version | vpn app | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------- | -------------------- |
| Apple | iPad mini 2 | 12.3.1 | OpenVPN Connect 3.0.2 | Passed by @rajannpatel | Passed by @rajannpatel |

### Full Tunnel VPN

| make | model | os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| Apple | iPad mini 2 | 12.3.1 | OpenVPN Connect 3.0.2 | Passed by @rajannpatel | Passed by @rajannpatel | Passed by @rajannpatel |

## Computers

### Split Tunnel VPN

| os version | vpn app | Test for a DNS Leak | Test the Ad Blocking |
| ---------- | ------- | ------------------- | -------------------- |
| macOS Sierra 10.12.6 | Tunnelblick 3.7.8 (build 5180) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/10#issuecomment-450702300) by @rknobbe | Passed by @rknobbe  |
| Windows 10 Home | Viscosity 1.7.14 (build 1595) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issuecomment-456246284) by @rajannpatel | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issuecomment-456246284) by @rajannpatel |

### Full Tunnel VPN

| os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| macOS Sierra 10.12.6 | Tunnelblick 3.7.8 (build 5180) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/10#issuecomment-450702300) by @rknobbe | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by @rknobbe | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by @rknobbe |
| Ubuntu 18.04 | - | Passed by @LucasHMS | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by @LucasHMS | Passed by @LucasHMS |
| Windows 10 Home | Viscosity 1.7.14 (build 1595) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by @rajannpatel | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by @rajannpatel | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by @rajannpatel |