# Pi-Hole and PiVPN on Google Compute Engine Free Tier with Full Tunnel and Split Tunnel OpenVPN Configurations

Run your own privacy-first ad blocking service in the cloud for free on Google Cloud Services. This guide shows you how to encrypt all your traffic, or just your DNS requests, over a VPN connection on your Android Phone.

# work in progress - check back often

<img src="./images/logos/cloud.svg" width="48" align="left">

# Google Cloud Login and Account Creation

Go to https://cloud.google.com and click **Console** at the top right if you have previously used Google's Cloud Services, or click **Try Free** if it's your first time.

 ### Account Creation
 - Step 1: Agree to the terms and continue.
 - Step 2: set up a payments profile and continue.
 ### Compute Engine Creation
 - Click the Hamburger Menu at the top left: <br><img src="./images/screenshots/1.png" width="294">
 - Click Compute Engine: <br><img src="./images/screenshots/2.png" width="279">

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

Run `shutdown -r now` to reboot.