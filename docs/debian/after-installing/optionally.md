---
layout: default
title: Optionally
nav_order: 224
has_children: false
parent: After Installing
grand_parent: Debian
permalink: /things-to-do-after-installing-debian-optionally

---
2022-02-08 11:36
# Things to do after installing Debian - optionally
{: .no_toc }
*ver. 22.02 Desktop Workstation*

<details close markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

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

### Install WebApp Manager
*...and add any website as a standalone system App*

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
