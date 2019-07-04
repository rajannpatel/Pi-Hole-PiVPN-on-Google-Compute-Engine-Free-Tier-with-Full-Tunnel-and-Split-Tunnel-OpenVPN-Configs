# Supported & Compatible Software Combinations

If you succeed or fail at implementing this OpenVPN solution on your device, please submit a Pull Request to this Repository with an update to the table below.

The tests columns refer to steps outlined under [Verify Everything Works](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs#verify-everything-works) in the **README.md** file.

## Phones

### Split Tunnel VPN

| make | model | os version | vpn app | Test for a DNS Leak | Test the Ad Blocking | Traffic Splitting |
| ---- | ----- | ---------- | ------- | ------------------- | -------------------- | ----------------- |
| Google | Pixel 3/3XL | Android 9 build# PQ3A.190605.003 | OpenVPN for Android 0.7.8 | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) |
| ? | ? | Android 6.0.1 | OpenVPN for Android (version?) | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/40) by [@Fliu777](https://github.com/Fliu777) | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/40) by [@Fliu777](https://github.com/Fliu777) | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/40) by [@Fliu777](https://github.com/Fliu777) |

### Full Tunnel VPN

| make | model | os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| Google | Pixel 3/3XL | Android 9 build# PQ3A.190605.003 | OpenVPN Connect 3.0.5 | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) |

## Tablets

### Split Tunnel VPN

| make | model | os version | vpn app | Test for a DNS Leak | Test the Ad Blocking | Traffic Splitting |
| ---- | ----- | ---------- | ------- | ------------------- | -------------------- | ----------------- |
| Apple | iPad mini 2 | 12.3.1 | OpenVPN Connect 3.0.2 | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) |

### Full Tunnel VPN

| make | model | os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---- | ----- | ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| Apple | iPad mini 2 | 12.3.1 | OpenVPN Connect 3.0.2 | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) | Passed by [@rajannpatel](https://github.com/rajannpatel) |

## Computers

### Split Tunnel VPN

| os version | vpn app | Test for a DNS Leak | Test the Ad Blocking | Traffic Splitting |
| ---------- | ------- | ------------------- | -------------------- | ----------------- |
| macOS Sierra 10.12.6 | Tunnelblick 3.7.8 (build 5180) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/10#issuecomment-450702300) by [@rknobbe](https://github.com/rknobbe) | Passed by [@rknobbe](https://github.com/rknobbe) | Passed by [@rknobbe](https://github.com/rknobbe) |
| Ubuntu 18.04 | gnome-manager | Passed by [@magarto](https://github.com/magarto) | Passed by [@magarto](https://github.com/magarto) | [Failed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16) by [@magarto](https://github.com/magarto) |
| Ubuntu 19.04 | gnome-manager | ? | [Passed](https://www.reddit.com/r/pihole/comments/bia2bv/started_long_term_traveling_and_didnt_set_up_vpn/em0y3do/) by [@mwoolweaver](https://www.reddit.com/user/mwoolweaver/) | ? |
| PopOS 18.10 | ? | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-487386686) by [@setzke](https://github.com/setzke) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-487386686) by [@setzke](https://github.com/setzke) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-487386686) by [@setzke](https://github.com/setzke) |
| Manjaro 18.04 | ? | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-491597505) by [@Kwbmm](https://github.com/Kwbmm) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-491597505) by [@Kwbmm](https://github.com/Kwbmm) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/16#issuecomment-491597505) by [@Kwbmm](https://github.com/Kwbmm) |
| Windows 10 Home | Viscosity 1.7.14 (build 1595) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issuecomment-456246284) by [@rajannpatel](https://github.com/rajannpatel) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issuecomment-456246284) by [@rajannpatel](https://github.com/rajannpatel) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issuecomment-456246284) by [@rajannpatel](https://github.com/rajannpatel) |

### Full Tunnel VPN

| os version | vpn app | Test your Full Tunnel VPN | Test for a DNS Leak | Test the Ad Blocking |
| ---------- | ------- | ------------------------- | ------------------- | -------------------- |
| macOS Sierra 10.12.6 | Tunnelblick 3.7.8 (build 5180) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/10#issuecomment-450702300) by [@rknobbe](https://github.com/rknobbe) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by [@rknobbe](https://github.com/rknobbe) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by [@rknobbe](https://github.com/rknobbe) |
| Ubuntu 18.04 | gnome-manager | Passed by [@LucasHMS](https://github.com/LucasHMS) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/22) by [@LucasHMS](https://github.com/LucasHMS) | Passed by [@LucasHMS](https://github.com/LucasHMS) |
| Ubuntu 19.04 | gnome-manager | ? | ? | [Passed](https://www.reddit.com/r/pihole/comments/bia2bv/started_long_term_traveling_and_didnt_set_up_vpn/em0y3do/) by [@mwoolweaver](https://www.reddit.com/user/mwoolweaver/) |
| Windows 10 Home | Viscosity 1.7.14 (build 1595) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by [@rajannpatel](https://github.com/rajannpatel) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by [@rajannpatel](https://github.com/rajannpatel) | [Passed](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues/18#issue-399133505) by [@rajannpatel](https://github.com/rajannpatel) |