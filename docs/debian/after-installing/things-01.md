---
layout: default
title: Regular
nav_order: 221
has_children: false
parent: After Installing
grand_parent: Debian
permalink: /things-to-do-after-installing-debian-regular

---

2022-02-07 14:54

# Things to do after installing Debian - regular
{: .no_toc }
*ver. 22.02_regular Desktop Workstation*

<details close markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Introduction

--- writing --- writing --- writing ---

---

## Installation medium

**Preferred:**
[Debian 11.2 Gnome Live non-free](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/11.2.0-live+nonfree/amd64/iso-hybrid/debian-live-11.2.0-amd64-gnome+nonfree.iso):

Download and flash the .iso image to USB thumb-drive, using Ventoy or Etcher and navigate through regular installation process.

---

## Initial configuration

### Add backports repository

```
sudo nano /etc/apt/sources.list.d/debian-backports.list
```

Add following:

```
# bullseye backports
deb http://ftp.debian.org/debian bullseye-backports main contrib non-free
deb-src http://ftp.debian.org/debian stretch-backports main
```

Save the file and exit

---

### Update the repositories

```
sudo apt update
```

---

### Remove default LibreOffice installation (deb) before upgrading

*(we will install LibreOffice Flatpak at the later stage)*

```
sudo apt remove --purge libreoffice*
```

---

### Remove default games

```
sudo apt remove iagno lightsoff four-in-a-row gnome-robots pegsolitaire gnome-2048 hitori gnome-klotski gnome-mines gnome-mahjongg gnome-sudoku quadrapassel swell-foop gnome-tetravex gnome-taquin aisleriot -y
```

---

### Remove Firefox-ESR

```
sudo apt remove --purge firefox*
```

---

### Upgrade the system

```
sudo apt upgrade -y

sudo apt dist-upgrade -y

sudo reboot
```

```
sudo apt autoremove && sudo apt autoclean
```

---

### Install SSH

```
sudo apt install openssh-server -y
```

---

### Install and configure Uncomplicated Firewall (ufw)

```
sudo apt install ufw

sudo ufw enable

sudo ufw default deny incoming

sudo ufw default allow outgoing

sudo ufw allow ssh

sudo apt install gufw
```

*for more configuration options visit: [Debian Wiki](https://wiki.debian.org/Uncomplicated%20Firewall%20(ufw))*

---

## Additional software installation

### Install essential apps

```
sudo apt install wget git curl neofetch mc ncdu tmux inxi htop thunderbird audacious audacity gimp inkscape krita darktable -y
```

---

### Install Vivaldi Web browser

```
wget https://downloads.vivaldi.com/stable/vivaldi-stable_5.0.2497.51-1_amd64.deb

sudo apt install ./vivaldi-stable_5.0.2497.51-1_amd64.deb
```

*...also, consider switching to [Brave Search Engine](https://search.brave.com/default)*.

*Here's why: [https://search.brave.com/help/independence](https://search.brave.com/help/independence)*

---

### Remove default games

```
sudo apt remove iagno lightsoff four-in-a-row gnome-robots pegsolitaire gnome-2048 hitori gnome-klotski gnome-mines gnome-mahjongg gnome-sudoku quadrapassel swell-foop gnome-tetravex gnome-taquin aisleriot -y
```

---

### Install Microsoft Base Fonts

for the basic Microsoft Font pack:

```
sudo apt install -y ttf-mscorefonts-installer fonts-crosextra-carlito fonts-crosextra-caladea
```

...or, if you have an access to Windows OS you can copy `C:\Windows\Fonts` directory for the **full** *Windows 10* default fonts directory, download following:
[Windows 10 Font Pack](https://pixeldrain.com/u/DJYYa8E9).
Create `.fonts` directory in your home location and copy your Windows fonts. 

---

### Make sure printer support is installed

```
sudo apt install skanlite cups cups-client cups-filters hplip printer-driver-hpijs

sudo adduser [USERNAME] lpadmin

sudo systemctl enable --now cups
```

*Replace [USERNAME] with your username*

---

### Install build-essential

It’s a package that includes many dependencies commonly used by different apps so it’s always good to have it installed. We all need it sooner or later.

```
sudo apt install build-essential dkms linux-headers-$(uname -r)
```

---

### Install restricted-extras

```
sudo apt install rar unrar libavcodec-extra gstreamer1.0-libav gstreamer1.0-plugins-ugly gstreamer1.0-vaapi
```

---

### Install Flatpak

```
sudo apt install flatpak

sudo apt install gnome-software-plugin-flatpak

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

sudo reboot
```

---

### Install LibreOffice flatpak version

```
flatpak install flathub org.libreoffice.LibreOffice

flatpak install --reinstall flathub org.freedesktop.Platform.Locale/x86_64/21.08
```

remember to change formats to Bulgarian in Language Settings

---

### Automate flatpak updates

*(yes, without sudo)*

```
crontab -e
```

add the line on the end:
`15 12 * * * flatpak update -y > /home/[USERNAME]/Documents/logs/flatpak-update.log`
*Replace [USERNAME] with your username*
(the log destination is custom, the directory must exsist)

### Install Syncthing

Add the release PGP keys:

```
sudo curl -s -o /usr/share/keyrings/syncthing-archive-keyring.gpg https://syncthing.net/release-key.gpg
```

Add the "stable" channel to your APT sources:

```
echo "deb [signed-by=/usr/share/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list
```

Update and install syncthing:

```
sudo apt update
```

```
sudo apt install syncthing
```

Enable syncthing at system boot:

```
sudo systemctle enable --now syncthing@[USERNAME].service
```

*Replace [USERNAME] with your username*

Edit line 59 in `config.xml` file, and replace `127.0.0.1` with `0.0.0.0`

```
nano /home/viking/.config/syncthing/config.xml
```

```
sudo systemctl restart syncthing@[USERNAME].service
```

*Replace [USERNAME] with your username*

Now, Syncthing is accessible under http://localhost:8384 and in the local network.

---

### Install NoMachine

*version from 2022-02-03*

```
wget https://download.nomachine.com/download/7.8/Linux/nomachine_7.8.2_1_amd64.deb
```

```
sudo apt install ./nomachine_7.8.2_1_amd64.deb
```

---

### Install ZeroTier One

```
curl -s https://install.zerotier.com | sudo bash
```

```
sudo zerotier-cli join [YOUR-ZEROTIER-NETWORK-ID]
```

---

### Install OpenConnect and OpenVPN

```
sudo apt install -y openconnect network-manager-openconnect network-manager-openconnect-gnome
```

```
sudo apt install -y openvpn network-manager-openvpn network-manager-openvpn-gnome
```

---

### Install AppImage Launcher

```
wget https://github.com/TheAssassin/AppImageLauncher/releases/download/v2.2.0/appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb
```

```
sudo apt install ./appimagelauncher_2.2.0-gha74.10c226a+bionic_amd64.deb
```

---

### Install TOR

enable the usage of https in sources.list:

```
sudo apt install apt-transport-https
```

add the Tor repository:

```
sudo sh -c 'echo "deb [arch=amd64] https://deb.torproject.org/torproject.org $(lsb_release -sc) main" >> /etc/apt/sources.list.d/tor-project.list'
```

download the latest keyring .deb package from the link below:

```
wget https://deb.torproject.org/torproject.org/pool/main/d/deb.torproject.org-keyring/deb.torproject.org-keyring_2020.11.18_all.deb
ls
```

install the keyring .deb package:

```
sudo apt install ./deb.torproject.org-keyring_2020.11.18_all.deb
```

update repos and upgrade your system:

```
sudo apt update && sudo apt upgrade
```

Install Tor:

```
sudo apt install tor
```

Check the status of the service (should be active):

```
systemctl status tor
```

is it dead? enable and run tor as service

```
sudo systemctl enable --now tor
```

Install Tor Browser:

```
sudo apt install torbrowser-launcher
```

---

### Install Wine and dependencies

```
sudo dpkg --add-architecture i386

wget -nc https://dl.winehq.org/wine-builds/winehq.key

sudo gpg -o /etc/apt/trusted.gpg.d/winehq.key.gpg --dearmor winehq.key

sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/debian/ bullseye main'

sudo apt update

sudo apt install --install-recommends winehq-staging

winecfg
```

---

### Install "Bottles", a brand new wine manager

```
flatpak install flathub com.usebottles.bottles
```

---

### Extend the Battery Life

If you have Debian installed on your laptop, you can squeeze more battery juice by installing tlp (power management tool).

```
sudo apt install tlp
```

---

### finishing up

```
sudo apt autoremove
```

```
sudo apt autoclean
```

\
\
\
.

---


*Reference:*

[https://wiki.debian.org](https://wiki.debian.org)

[https://packages.debian.org/bookworm/nvidia-legacy-390xx-driver](https://packages.debian.org/bookworm/nvidia-legacy-390xx-driver)

[https://www.linuxcapable.com/debian](https://www.linuxcapable.com/debian/)

*Don't break your Debian!*

[https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian](https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian)
