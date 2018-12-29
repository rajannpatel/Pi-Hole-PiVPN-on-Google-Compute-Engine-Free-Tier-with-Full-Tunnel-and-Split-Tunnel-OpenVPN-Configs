# Pi-Hole and PiVPN on Google Compute Engine Free Tier with Full Tunnel and Split Tunnel OpenVPN Configurations

<img src="./images/data-privacy-risk.svg" width="125" align="right">

The goal of this guide is to enable you to safely and privately use the Internet on your phone without intrusive advertisements, and blocking your ISP, mobile carrier, or public Wi-Fi hotspot provider from gaining insight into your usage activity.

<img src="./images/upfront-cost.svg" width="90" align="right">

Run your own privacy-first ad blocking service within the [Free Usage Tier](https://cloud.google.com/free/) on Google Cloud. This guide gets you set up with a Google Cloud account, and walks you through setting up a full tunnel (all traffic) or split tunnel (DNS traffic only) VPN connection on your Android Phone.

The benefit of a Split Tunnel VPN is that you can still interact with devices on your Local Network (such as Chromecast) and still have DNS based ad-blocking over an encrypted connection to the cloud.

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
- Enable billing for this Project if you haven't already: <br><img src="./images/screenshots/6.png" width="288">
- Compute Engine will begin initializing: <br><img src="./images/screenshots/7.png" width="232">

<img src="./images/logos/computeengine.svg" width="48" align="left">

# Compute Engine Virtual Machine Setup

- Create a Virtual Machine instance on Compute Engine: <br><img src="./images/screenshots/8.png" width="216">
- Customize the instance: <br><img src="./images/screenshots/8.png" width="216">
- Name your Virtual Machine **pi-hole**. <br>Your Region selection should be any US region only (excluding Northern Virginia [us-east4]). I have used **us-east1** and the **us-east1-b** zone because it is closest to me. <br>Choose a **micro** Machine Type in the dropdown. <br>Change the **Boot Disk** to be **30GB** if you plan on keeping your DNS lookup records for any reason, otherwise the default **10GB** disk allocation is adequate. <br>**Allow HTTPS traffic** in the Firewall (add a checkmark). <br><img src="./images/screenshots/9.png" width="232">
- Expand **Management, Security, disks, networking, sole tenancy** and click the "Network" tab. Click the Pencil icon under "Network Interfaces". <br><img src="./images/screenshots/10.png" width="238">
- Reserve a Static Internal IP Address for your Primary Internal IP. <br><img src="./images/screenshots/11.png" width="222"> <br><img src="./images/screenshots/12.png" width="260">
- The External IP Address should not be Ephemeral. Reserve a New Static IP Address <br><img src="./images/screenshots/13.png" width="230"> <br><img src="./images/screenshots/14.png" width="395">
- You can log into your Virtual Machine via SSH in a Browser by clicking the SSH button. <br><img src="./images/screenshots/15.png" width="369">
- Click the Hamburger Menu at the top left, click **VPC Network** and click **Firewall Rules**. <br><img src="./images/screenshots/firewall.png" width="222"> <br>Click **Create Firewall Rule** at the top center of the page. The name of your rule should be `allow-openvpn`, change the **Targets** dropdown to **All instances in the network**. The **Source IP Ranges** should be `0.0.0.0/0`. The **udp** checkbox should be selected, and the port number next to it should be changed from `all` to `1194`. Then click the **Create** button.

<img src="./images/logos/debian.svg" width="48" align="left">

# Debian Update & Upgrade

Once you log into your Virtual Machine via SSH, you want to update and upgrade it.

```
sudo su
apt-get update && apt-get upgrade -y
```

<img src="./images/logos/pihole.svg" width="48" align="left">

# Pi-Hole Installation

```
sudo su
curl -sSL https://install.pi-hole.net | bash
```

You will flow into a series of prompts in a blue screen.

- Choose OK or answer positively for all the prompts until the "Select Protocols" question appears. IPv6 needs to be deselected as shown below: <br><img src="./images/screenshots/16.png" width="281">

Choose OK or answer positively for all the other prompts.

- Go to the Web Interface, log in, and click **Settings**, and navigate to **DNS**. <br>Set your **Interface Listening Behavior** to **Listen on All Interfaces** on this page: <br><img src="./images/screenshots/18.png" width="237">

<img src="./images/logos/pivpn.png" width="48" align="left">

# PiVPN Installation

```
sudo su
curl -L https://install.pivpn.io | bash
```

You will flow into a series of prompts in a blue screen. All of the default values are appropriate. Choose OK or answer positively for all the prompts until you have to choose an upstream DNS provider. The default answer is Google. Choose **Custom** and set an IP Address of **10.8.0.1**

The default answer to reboot is **No** at the end of the installer. It is fine to say **No**, we have a few more things to edit while we're logged in as root.

<img src="./images/logos/openvpn.svg" width="48" align="left">

# OpenVPN Configuration

Get into the openvpn directory:

```
sudo su
cd /etc/openvpn
```

Edit **server.conf**. I prefer to use **nano**, so the command would be:

```
nano server.conf
```

Comment out the line which reads `push "redirect-gateway def1"` so it reads as follows:

```
# push "redirect-gateway def1"
```

The longer the keep-alive interval the longer it will take either end of the openvpn connection to detect whether the connection is no longer alive. Because mobile devices often lose connectivity and regain it, lower values are desirable.

Comment out `keepalive 1800 3600` and add `keepalive 10 60` below it, so it appears as follows:

```
# keepalive 1800 3600
keepalive 10 60
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

Press `CTRL` `O` to bring up the save prompt at the bottom of Nano, press **Enter** to save. Then press `CTRL` `X` to exit



To accept incoming OpenVPN connections over TCP on port 443:

```
sudo su
cd /etc/openvpn/
cp server.conf server_tcp443.conf
```

Edit **server_tcp443.conf**. I prefer to use **nano**, so the command would be:

```
nano server_tcp443.conf
```

Replace the `proto udp` and `port 1194` lines with:

```
proto tcp
port 443
```

Edit the `server 10.8.0.0 255.255.255.0` line to reflect an IP address of **10.9.0.0**, so it reads as follows:

```
server 10.9.0.0 255.255.255.0
```

Above the line `push "dhcp-option DNS 10.8.0.1"` add `push "route 10.8.0.1"` so it reads as follows:

```
push "route 10.8.0.1"
push "dhcp-option DNS 10.8.0.1"
```

Comment out `keepalive 10 60` and add `keepalive 10 120` below it, so it appears as follows:

```
# keepalive 1800 3600
keepalive 10 120
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

<img src="./images/logos/pivpn.png" width="48" align="left">

# Managing the PiVPN

Connect to the Pi-Hole server and set up an OpenVPN Client Profile

```
pivpn add nopass
```

Give your client a name. I like to use an alphanumeric string composed of the user's first name, and their device's make and model (no spaces and no special characters).

This command will output a success message which looks like this:

```
========================================================
Done! mypixel3xl.ovpn successfully created! 
mypixel3xl.ovpn was copied to:
  /home/myusername/ovpns
for easy transfer. Please use this profile only on one
device and create additional profiles for other devices.
========================================================
```

To get the **mypixel3xl.ovpn** file to your phone it is easiest to maximize your SSH window and print the file to the terminal window, to copy & paste the output:

```
cat /home/myusername/ovpns/mypixel3xl.ovpn
```

Press `CTRL` `-` until the screen zooms out to a point where you can see the entire ovpn file printed on the screen. The first line will have the word `client` and the last line is `</tls-crypt>`. Highlighting this entire chunk with a mouse will cause a scissor icon to appear in the middle of your SSH window, this means this selection has been copied to your clipboard.

Paste this into your favorite Text Editor and save the file with an **.ovpn** extension.

Around Line 12, edit the line which reads `cipher AES-256-CBC` and change it to read:

```
cipher AES-128-GCM
```

E-mail the file to yourself, upload in Google Drive, or use whatever secure method you prefer to transfer this file to your phone. This file can be downloaded to your phone.

<img src="./images/logos/openvpnforandroid.svg" width="48" align="left">

# OpenVPN for Android

<a href="https://f-droid.org/repository/browse/?fdid=de.blinkt.openvpn" target="_blank">
<img src="https://f-droid.org/badge/get-it-on.png" alt="Get it on F-Droid" height="80"/></a>
<a href="https://play.google.com/store/apps/details?id=de.blinkt.openvpn" target="_blank">
<img src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png" alt="Get it on Google Play" height="80"/></a>

## Client Configuration for Split Tunnel VPN

When the app opens you are in the **Profiles** Tab.
- Import your Profile, click the `+` at the top right.
- Then click **Import** at the bottom left of the modal that appears.
- Click the Hamburger Menu at the top left to choose **Google Drive**, or your **Downloads** folder, depending on what method you used to get the **.ovpn** file to your phone.
- Click the pencil icon next to the VPN profile you imported.
  - Click the **Routing** Tab.
    - Click **Excluded Networks** under IPv4 and add this:
      ```
      10.0.0.8/8 172.16.0.0/12 192.168.0.0/16
      ```
    - **Bypass VPN for local networks** should NOT have a checkmark. Uncheck it.
    - Under the **Authentication/Encryption** Tab
      - The **Encryption Cipher** should be `AES-128-GCM`
    - Under the **Allowed Apps** Tab
      - the **Drive**, **Duo**, **Gmail**, **Google Play Store**, **Phone**, **Phone and Messaging Storage** and **Phone Services** apps should have a checkmark.

- Click the back button a couple times until you are at the **Profiles** Tab again.

Click the **Settings** Tab:
- **OpenVPN 3 Core** should have a checkmark
- click **Default VPN** and choose the VPN you have imported
- **Connect on Boot** should have a checkmark

Click the back button a couple times until you are at the **Profiles** Tab again.
- Clicking the name of the VPN profile you imported should trigger a connection.

## Client Configuration for Full Tunnel VPN

This is a work in progress. Full Tunnel VPN instructions will be coming soon.

# Contributions Welcome

If there is something that can be done better, or if this documentation can be improved in any way, please submit a Pull Request with your fixes or edits. Discussions regarding [Issues](https://github.com/rajannpatel/Pi-Hole-PiVPN-on-Google-Compute-Engine-Free-Tier-with-Full-Tunnel-and-Split-Tunnel-OpenVPN-Configs/issues) are welcome as well.