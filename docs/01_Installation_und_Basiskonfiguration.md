# Installation und Basiskofiguration

## Systemübersicht

**Gerät:** Raspberry Pi 400 ( aarch64 )
**System:** Arch Linux Arm
**Init-System:** systemd ( Standart )
**Shell:** Bash 5.3.3 (  bei Ersteinrichtung )
**TTY-only:** Kein Display-Manager oder GUI, direkter Login in die Konsole
**Primäre Nutzung:** Lernlabor & Build-Maschine

---

## Installation

Das Grundsystem basiert auf dem offiziellem **Arch Linux ARM Image** für den Raspberry Pi 4.
- [archlinuxarm.org](https://archlinuxarm.org)

Die Installation erfolgte manuell, indem die Micro-SD-Karte vorebereitet und anschließend das Image entpackt und kopiert wurde.

---

### Partitionierung

| Partition | Größe | Dateisystem | Beschreibung |
| --------- | ----- | ----------- | ------------ |
| `/boot`   | 1 GB  | FAT32 (W95) | Enthält Kernel, Bootloader und Firmware |
| `/` | Restlicher Speicherplatz | ext4 | Root-Dateisystem |

> **Hinweis:** Die Boot-Partition wurde bewusst auf 1 GB vergrößert ( Standart 200 MB reichen oft nicht aus ).

---

### Boot & Login

Nach dem Bootvorgang erscheint direkt die Login-Aufforderung auf der TTY, ohne Display-Manager oder grafische Oberfläche.

---

## Basispakete & Werkzeuge

Das erste installierte Paket war selbstverständlich:

```bash
pacman -S fastfetch
```
... für die standesgemäße Begrüßung nach dem Login.


Der Vollständigkeit und Reproduzierbarkeithalber hier aber eine vollständige Liste der von mir hinzugfügten Pakete:

> Liste erstellt mit `pacman -Qe`

```bash
archlinuxarm-keyring
base
base-devel
btop
dhcpcd
dialog
fastfetch
firmware-raspberrypi
git
glow
linux-aarch64
luarocks
man-db
man-pages
man-pages-de
most
nano
neovim
net-tools
netctl
openssh
raspberrypi-bootloader
shellcheck
sudo
tldr
tmux
tmux-plugin-manager
tmux-resurrect
uboot-raspberrypi
uboot-tools
vi
w3m
wget
which
wireless-regdb
wireless-tools
wpa-supplicant
yay
ntp
```
---

## Netzwerk

Die WLAN-Verbindung wurde über ein manuell konfiguriertes netctl-Profil eingerichtet und so eingestellt, das sie automatisch beim Booten verbunden wird.

Hier ein kurzes Snippet zu Orientierung:


```bash
/etc/netctl# install -m640 examples/wireless-wpa <Name der Verbindung>
/etc/natctl# cat <Name der Verbindung>
Description='A simple WPA encrypted wireless connection'
Interface=wlan0
Connection=wireless
Security=wpa

IP=dhcp

ESSID='MyNetwork'
# Prepend hexadezimal keys with \"
# If your key starts with ", write it as '""<key>"'
# See also: the section on special quoting rules in betctl.profile(5)
Key='WirelessKey'
# Uncomment this if your ssid is hidden
# Hidden=yes

```
Starten der angelegten Verbindung mit `netctl start <Namer der Verbindung>`

Die Verbindung automatisch nach dem Booten starten mit `netctl enable <Name der Verbindung>`

---

## Benutzerverwaltung

- **Root-Zugang**: Nur für das initiale Setup verwendet
- **Regulärer Benutzer**: Arbeitet mit `sudo`
- **TTYs:** Hauptsächlich TTY 1-2 aktiv
- ( durch tmux-Setup keine weiteren Sessions notwendig )

---

## Nutzungkonzept

Das System fungiert als **mobiles ArchPi-Lernlabor.**
Ziele sind:

- Training der Arbeit in einer reinen Konsolenumgebung.
- Verständnis manueller Kompilation
- Übung in Bash-Scripting und Tool-Automatisierung
- Schrittweise Integration von Markdown-basierten Notizen 
