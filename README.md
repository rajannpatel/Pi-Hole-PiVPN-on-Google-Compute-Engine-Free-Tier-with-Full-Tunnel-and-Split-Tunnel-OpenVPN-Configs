# work in progress - check back often

# Pi-Hole and PiVPN on Google Compute Engine Free Tier with Full Tunnel and Split Tunnel OpenVPN Configurations

<img src="./images/data-privacy-risk.svg" width="125" align="right">

The goal of this guide is to enable you to safely and privately use the Internet on your phone without intrusive advertisements, and blocking your ISP, mobile carrier, or public Wi-Fi hotspot provider from gaining insight into your usage activity.

<img src="./images/upfront-cost.svg" width="90" align="right">

Run your own privacy-first ad blocking service within the Free Usage Tier on Google Cloud. This guide gets you set up with a Google Cloud account, and walks you through setting up a full tunnel (all traffic) or split tunnel (DNS traffic only) VPN connection on your Android Phone.

| Tunnel Type | Data Usage | Security | Ad Blocking |
| -- | -- | -- | -- |
| full | 10% more data usage | 100% encryption | yes
| split | least data usage | DNS encryption only | yes

---

<img src="./images/logos/cloud.svg" width="48" align="left">

# Google Cloud Login and Account Creation

Go to https://cloud.google.com and click **Console** at the top right if you have previously used Google's Cloud Services, or click **Try Free** if it's your first time.

 ### Account Creation
 - **Step 1 of 2** <br> Agree to the terms and continue. <br><img src="./images/screenshots/5.png" width="265">
 - **Step 2 of 2** <br> Set up a payments profile and continue <br><img src="./images/screenshots/5.png" width="223">
 ### Project & Compute Engine Creation
 - Click the Hamburger Menu at the top left: <br><img src="./images/screenshots/1.png" width="197">
 - Click **Compute Engine**: <br><img src="./images/screenshots/2.png" width="138">
 - Select **VM instances**: <br><img src="./images/screenshots/3.png" width="102">
 - Create a Project if you don't already have one: <br><img src="./images/screenshots/4.png" width="294">
 - 

<img src="./images/logos/computeengine.svg" width="48" align="left">

# Compute Engine Steps

lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor

<img src="./images/logos/debian.svg" width="48" align="left">

# Debian Steps

```
sudo su
apt-get update && apt-get upgrade -y
```

<img src="./images/logos/pihole.svg" width="48" align="left">

# Pi-Hole Steps

```
curl -sSL https://install.pi-hole.net | bash
```

You will flow into a series of prompts in a blue screen. All of the default values are appropriate.

Choose OK or answer positively for all the prompts until the network questions appear:

 - ipv6 needs to be deselected

Choose OK or answer positively for all the other prompts.

<img src="./images/logos/pivpn.png" width="48" align="left">

# PiVPN Steps

```
curl -L https://install.pivpn.io | bash
```

You will flow into a series of prompts in a blue screen. All of the default values are appropriate. Choose OK or answer positively for all the prompts until you have to choose an upstream DNS provider. The default answer is Google. Choose **Custom** and set an IP Address of **10.8.0.1**

The default answer to reboot is **No** at the end of the installer. It is fine to say **No**, we have a few more things to edit while we're logged in as root.

<img src="./images/logos/openvpn.svg" width="48" align="left">

# OpenVPN Steps

Get into the openvpn directory:

```
cd /etc/openvpn
```

I prefer to use **nano**, so the command would be:

```
nano server.conf
```

Comment out the line which reads `push "redirect-gateway def1"` so it reads as follows:

```
# push "redirect-gateway def1"
```

The longer the keep-alive interval the longer it will take either end of the openvpn connection to detect whether the connection is no longer alive. Because mobile devices often lose connectivity and regain it, lower values are desirable.

Comment out `keepalive 1800 3600` and add `keepalive 10 120` below it, so it appears as follows:

```
# keepalive 1800 3600
keepalive 10 120
```

Comment out the line which reads `cipher AES-256-CBC` and add `cipher AES-128-GCM` below it, so it reads as follows:

```
# cipher AES-256-CBC
cipher AES-128-GCM
```

At the bottom of the file add the following lines:

```
# performance stuff
fast-io
compress lz4-v2
push "compress lz4-v2"
```

Press `CTRL`+`O` to bring up the save prompt at the bottom of Nano, press **Enter** to save. Then press `CTRL`+`X` to exit



To accept incoming OpenVPN connections over TCP on port 443:

```
cd /etc/openvpn/
cp server.conf server_tcp443.conf
```

`nano server_tcp443.conf` and make these edits:

Replace the `proto udp` and `port 1194` lines with:

```
proto tcp
port 443
```

Edit the `server 10.8.0.0 255.255.255.0` line to reflect an IP address of **10.9.0.0**

```
server 10.9.0.0 255.255.255.0
```

Above the line `push "dhcp-option DNS 10.8.0.1"` add this line so it reads as follows:

```
push "route 10.8.0.1"
push "dhcp-option DNS 10.8.0.1"
```

Comment out `fast-io` so it looks like this:

```
# fast-io
```

Add the OpenVPN service on Port 443:

```
systemctl enable openvpn@server_tcp443.service
```

Reboot the server with this shutdown command:

```
shutdown -r now
```

<img src="./images/logos/openvpnforandroid.svg" width="48" align="left">

# OpenVPN for Android

