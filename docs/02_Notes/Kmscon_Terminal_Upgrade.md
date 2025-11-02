# Kmscon Terminal Upgrade Versuch

## Was ist das Ziel?
**Zielvorgabe:** Beim Systemstart soll, möglichst unauffällig und unbemerkt, statt in die TTY in den `kmscon` Terminal Emulator gesprungen werden. Dies soll so nahtlos geschehen das das einem unwissenden gar nicht auffällt.

## Wie bin ich genau vorgegangen?
Im Kern habe ich folgende Schritte durchgeführt.

    1. Paket aus der Arch User Repository runterladen und kompilieren.
    2. Meinen ArchPi400 mit den passenden Ordner ausstatten und mit Schriftarten versorgen.
    3. Nach erfolgreichen Tests einen System-Dienst anlegen der dann das automatische starten übernimmt. 

## Wie habe ich das genau umgesetzt?

1. **Runterladen des Paketes mit anschließendem Kompilieren**
    Hier hat der befehl `yay -S kmscon` die komplette Arbeit übernommen. Trotz zahlreicher Warnhinweise das meine Architektur von dem Paket nicht unterstützt wird lief das Kompilieren ohne weitere Fehlermeldungen, sodass ich das Paket reibungslos in mein System integrieren konnte.

2. **Die passende Ordnerstruktur für Systemweite Fonts**
    Hier habe ich manuell mit dem Befehl `mkdir -p /usr/share/fonts/` die passende Struktur angelegt damit Arch die Schriftarten auch findet. Nach der Installation der Schriftarten ist mir aufgefallen das ich den Befehl `fc-cache` gar nicht zur Verügung habe. Dies hab ich dann schnell mit `sudo pacman -S fontconfig` korrigiert und im Anschluss dann den Fontcache mit `sudo fc-cache -vf` aktualisiert. Kurz mit `fc-list` überprüft ob alles passt und damit is dieser Schritt auch erledigt.

3. **Diesen Schritt habe ich bei mir noch nicht umgesetzt da ich bei meinen Testläufen kein zufriedenstellendes Ergebnis Erzeugen konnte. Dies wird Nachgetragen sollte ich ihn mal irgendwo vollständig einrichten und nutzen.**
