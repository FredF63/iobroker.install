# iobroker.install
Doku preview



# Installation von ioBroker unter Linux
---
Die Installationsanleitung hilft auch Einsteigern, die sich bisher wenig mit Linux beschäftigt haben!

Bitte nicht von der Länge dieser Anleitung abschrecken lassen - es werden hier verschiedene Möglichkeiten je nach verwendeter Hardware beschrieben.

Im Prinzip besteht **jede** Installation aus nur zwei Schritten:
* Installation eines Betriebssystems
* gemeinsame Installation von node.js und ioBroker per Einzeiler

Die weitere Verfahrensweise ist anschließend unabhängig von der verwendeten Hardware.



## Raspberry Pi und Einplatinencomputer (kurz SBC)

** benötigte Software/Hardware**
Für die Installation und die spätere Administrierung des ioBroker Systems werden folgende Komponenten benötigt:
* PC mit SD-Card Reader
* SD Karte (idealerweise Application Class 2 (A2) mit mind. 32GB)
* Schreibprogramm für SD-Karten (z.B. Balena etcher oder https://rufus.ie/)
* Terminalprogramm für SSH-Zugriff (z.B. puTTY)
* Hardware auf der ioBroker laufen soll mit mindestens 2GB RAM


** Betriebssystem **
Es wird empfohlen ein Debian basierendes Betriebssystem als **Server**, also ***ohne*** Desktop zu installieren.

* für einen Raspberry Pi: https://www.raspberrypi.org/software/operating-systems/
* für andere ARM-basierte Einplatinencomputer: https://www.armbian.com/download/

### Installationsablauf SBC

1. Das gewünschte Betriebssystem wird in der zum SBC passenden Version am PC heruntergeladen, 
gegebenfalls entpackt und auf die SD-Karte geschrieben.
> Beim Raspberry Pi muss nach dem Schreiben der SD-Karte noch auf der Bootpartition
> eine leere Datei mit Namen `ssh` ohne Dateiendung angelegt werden. 
> Dazu unter Windows mit der rechten Maustaste in dem Laufwerk der SD mit der 
> Bezeichnung `Boot` eine neue Textdatei anlegen und die Endung `.txt` löschen, 
> auch wenn Windows eine Meldung bringt.

2. Die SD-Karte anschließend in den SBC stecken und den SBC mit dem Netzwerk und der 
Stromversorgung verbinden.
Nach kurzer Zeit ist der SBC hoch gefahren und im Netzwerk erreichbar. Im Router 
nach dessen IP-Adresse suchen, und diese dabei direkt an den SBC binden.

3. Über das Terminalprogramm zum SBC verbinden, indem die IP des SBC unter Port 22 aufgerufen wird und die Zugangsdaten eingeben

#### Einrichtung und Aktualisierung des Systems
##### User anlegen
Sollte in dem System der Zugang mit *root* stattfinden und noch kein normaler User angelegt sein, muss dieser angelegt werden mit `adduser UserName` wobei UserName durch den gewünschen Usernamen ersetzt werden muss.

Anschließend das Passwort vergeben, wiederholen und bestätigen, dann mit `exit` ausloggen und eine neue Verbindung als User aufbauen.

##### Aktualisierung des Systems
Auch wenn das Betriebssystem neu heruntergeladen wurde sollte es auf Aktualisierung überprüft werden. Dies geschieht mit `sudo apt update && sudo apt upgrade`

Anschließend noch bestätigen.

Nach einiger Zeit ist das System auf dem neuesten Stand.

##### Konfiguration des Systems
Wichtige Einstellungen wie z.B.
* Zeitzone
* Sprache
* Servername
müssen über dem Aufruf `sudo raspi-config` bzw. `sudo armbian-config` eingestellt werden.
Danach nochmals rebooten mit `sudo reboot`

### Debian-PC
* Das Betriebssystem wird auf einen Bootfähigen USB-Stick geschrieben.
* Im BIOS wird
  * der Boot von USB aktiviert 
  * Auf ein "Legacy-Betriebssystem" umgestellt
  
Anschließend vom USB-Stick booten und der geführten Installation folgen.

Auch hier sollte keine grafische Oberfläche installiert werden.

* für einem (mini-) PC: https://www.debian.org/distrib/

## Installation von node.js und ioBroker

ioBroker wird mit dem Befehl `curl -sLf https://iobroker.net/install.sh | bash - ` installiert

Auf einem neuen System, auf dem sich noch kein node.js befindet wird dieses in der jeweils aktuell empfohlenen Version mit installiert.

---

## Nutzung von ioBroker
Die erfolgreiche Installation endet mit der Information unter welcher IP ioBroker aufgerufen werden soll. Unter dieser <IP>:8081 ist die Bedienoberfläche (der Admin) von ioBroker in jedem Browser aufrufbar.
