---

layout: default
title: After installing - reckless
nav_order: 102
has_children: false
parent: Debian
permalink: /things-to-do-after-installing-debian-reckless

---

![Debian](https://www.debian.org/Pics/debian-logo-1024x576.png)

2022-02-07 16:30

# Things to do after installing Debian - reckless

*ver. 22.02_reckless Desktop Workstation (still more stable than Arch btw)*

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
---

## 1. Installation medium:

**Preferred:**
[Debian 11.2 Gnome Live non-free](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/11.2.0-live+nonfree/amd64/iso-hybrid/debian-live-11.2.0-amd64-gnome+nonfree.iso):

Download and flash the .iso image to USB thumb-drive, using Ventoy or Etcher and navigate through regular installation process.

---

## 2. Initial configuration

### Replace repositories to "sid"

```
sudo mv /etc/apt/source.list /etc/apt/source.list.old

sudo nano /etc/apt/source.list
```

add following:

```
deb http://deb.debian.org/debian sid main contrib non-free
# deb-src http://deb.debian.org/debian sid main
```

save the file and exit

---

### Update the repositories

```
sudo apt update
```

---

### Remove default LibreOffice installation (deb) before upgrading

*(we will install LibreOffice Flatpak at the later stage):*

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
sudo apt remove firefox-esr
```

---

### Upgrade to Debian Sid

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

## 3. Additional software installation

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

...or, if you have an access to Windows OS you can copy `C:\Windows\Fonts' directory for the **full** *Windows 10* default fonts directory, download following:
[Windows 10 Font Pack](https://pixeldrain.com/u/DJYYa8E9).
Create `.fonts` directory in your home location and copy your Windows fonts. 

---

### Make sure printer support is installed

```
sudo apt install skanlite cups cups-client cups-filters hplip printer-driver-hpijs

sudo adduser [USERNAME] lpadmin

sudo systemctl enable --now cups
```

*Replace [USERNAME] with your user name*

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
*Replace [USERNAME] with your user name*
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

*Replace [USERNAME] with your user name*

Edit line 59 in `config.xml` file, and replace `127.0.0.1` with `0.0.0.0`

```
nano /home/viking/.config/syncthing/config.xml
```

```
sudo systemctl restart syncthing@[USERNAME].service
```

*Replace [USERNAME] with your user name*

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

### Install "Bottles"

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

## 4. Optionally

### Add locale
*preferably, do it before installing any apps*

```
sudo locale-gen bg_BG.UTF.8

sudo update-locale LANG=bg_BG.UTF-8

sudo locale-gen
```
*`bg_BG.UTF.8` used as an example*

If, for some reason that method doesn't work, uncoment your locale from `/etc/locale.gen` and then:

```
sudo locale-gen
```

Don't forget to change language, time and locale settings in the GUI system settings + **add BG keyboard layout**

---

### Install tweaked Linux Kernel

```
curl 'https://liquorix.net/add-liquorix-repo.sh' | sudo bash

sudo apt install linux-image-liquorix-amd64 linux-headers-liquorix-amd64
```

---

### Need some Apps?

```
flatpak install flathub net.cozic.joplin_desktop
```
Joplin is a free, open source note taking and to-do application, which can handle a large number of notes organised into notebooks. The notes are searchable, can be copied, tagged and modified either from the applications directly or from your own text editor. The notes are in Markdown format.

```
flatpak install flathub org.telegram.desktop
```
Pure instant messaging — simple, fast, secure, and synced across all your devices. One of the world's top 10 most downloaded apps with over 500 million active users.

```
flatpak install flathub io.freetubeapp.FreeTube
```
FreeTube is an open source desktop YouTube player built with privacy in mind. Use YouTube without advertisements and prevent Google from tracking you with their cookies and JavaScript.

```
flatpak install flathub com.stremio.Stremio
```
Watch videos, movies, TV series and TV channels instantly.

```
flatpak install flathub org.onlyoffice.desktopeditors
```
Create, view and edit text documents, spreadsheets and presentations of any size and complexity. Work on documents of most popular formats: DOCX, ODT, XLSX, ODS, CSV, PPTX, ODP, etc. Deal with multiple files within one and the same window thanks to the tab-based user interface.

```
https://flathub.org/apps/details/com.belmoussaoui.Decoder
```
Decoder is a fancy yet simple QR Codes scanner and generator.

```
flatpak install flathub org.gnome.Solanum
```
Solanum is a time tracking app that uses the pomodoro technique. Work in 4 sessions, with breaks in between each session and one long break after all 4.

```
https://flathub.org/apps/details/fr.romainvigier.MetadataCleaner
```
Metadata Cleaner allows you to view metadata in your files and to get rid of it, as much as possible.

```
flatpak install flathub com.github.tchx84.Flatseal
```
Flatseal is a graphical utility to review and modify permissions from your Flatpak applications.

---

### Install WebApp Manager and add any website as a standalone system App

(working best with Chromium engine based web browsers)

```
wget http://packages.linuxmint.com/pool/main/w/webapp-manager/webapp-manager_1.1.9_all.deb

sudo apt install python3-pip

pip install pillow

sudo apt install ./webapp-manager_1.1.9_all.deb
```

---

### Better Apperance

```
sudo apt install git && git clone https://github.com/vinceliuice/Tela-icon-theme.git

cd Tela-icon-theme

sudo ./install.sh -a
```

```
sudo apt install materia-gtk-theme
```

...and apply those changes in Gnome Tweaks 

---

### Using legacy Nvidia Geforce GPU?

```
sudo apt install nvidia-legacy-390xx-driver
```

\
\
\
.

---

---

*Reference:*

[https://wiki.debian.org](https://wiki.debian.org)

[https://packages.debian.org/bookworm/nvidia-legacy-390xx-driver](https://packages.debian.org/bookworm/nvidia-legacy-390xx-driver)

[https://www.linuxcapable.com/debian](https://www.linuxcapable.com/debian/)

*Don't break your Debian!*

[https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian](https://wiki.debian.org/DontBreakDebian#Don.27t_make_a_FrankenDebian)
