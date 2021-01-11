# iobroker.install
Doku preview



# Installation von ioBroker unter Linux

Diese Anleitung ermöglicht auch Einsteigern, die sich bisher wenig mit Linux beschäftigt haben, ioBroker in kürzester Zeit zu installieren!

ioBroker funktioniert auf vielen Linux Distributionen, dennoch wird  ein Debian basiertes Betriebssystem empfohlen.  
Da ioBroker über Browser oder Terminal administriert wird, sollte das Betriebssystem als **Server**, also ***ohne*** Desktop installiert werden.

Als Hardware kann ein Raspberry Pi, ein ARM-basierter Einplatinencomputer oder jeder Linux fähige PC mit Netzwerkanschluß genutzt werden.  
> Der Arbeitsspeicher sollte mindestens 2GB betragen.  

> Aus performancegründen sollte die Anbindung ins Netzwerk per LAN erfolgen

Im Prinzip besteht dann **jede** Installation aus sehr einfachen Schritten:
* Installation eines Betriebssystems und anschließender Anpassung
* gemeinsame Installation von node.js und ioBroker per Einzeiler
---
**benötigte Software/Hardware**

Für die Installation und die spätere Administrierung des ioBroker Systems werden 
folgende Komponenten benötigt:
* PC mit SD-Card Reader
* Packprogramm zum entpacken heruntergeladener Dateien (z.B. 7zip) 
* Schreibprogramm für SD-Karten (z.B. Balena etcher oder https://rufus.ie/)
* Terminalprogramm für SSH-Zugriff (z.B. puTTY)
* SD Karte (idealerweise Application Class 2 (A2) mit mind. 32GB)
* Hardware auf der ioBroker laufen soll


## Installationsablauf Raspberry Pi

1. Die Version **Raspberry Pi OS Lite** von https://www.raspberrypi.org/software/operating-systems/ herunter laden, entpacken und mit dem Schreibprogramm für SD-Karten auf die SD-Karte schreiben.

2. Beim Raspberry Pi muss nach dem Schreiben der SD-Karte noch auf der Bootpartition eine leere Datei mit Namen `ssh` ohne Dateiendung angelegt werden. Dazu unter Windows mit der rechten Maustaste in dem Laufwerk der SD mit der Bezeichnung `Boot` eine neue Textdatei anlegen und die Endung `.txt` löschen, auch wenn Windows eine Meldung bringt.
> ohne diese Datei ist der Pi später nicht über das Terminalprogramm erreichbar!

3. Die SD-Karte anschließend in den Pi stecken und den Pi mit dem Netzwerk und der Stromversorgung verbinden. Nach kurzer Zeit ist der Pi hoch gefahren und im Netzwerk erreichbar. Im Router nach dessen IP-Adresse suchen und, damit der Pi immer mit der gleichen IP Adresse erreichbar ist, diese dabei direkt an den Pi binden.

4. Über das Terminalprogramm zum Pi verbinden, indem die IP des Pi unter Port 22 aufgerufen wird und die Zugangsdaten eingeben werden:

	* User "pi", Passwort "raspberry"

5. Systemaktualisierung mit dem Befehl `sudo apt update && sudo apt upgrade` und anschließendem Enter durchführen. Eventuell muss noch eine Bestätigung mit `y` erfolgen. Nach einiger Zeit ist das System aktualisiert und auf dem neuesten Stand.

6. Über dem Aufruf `sudo raspi-config` am  Raspberry Pi folgende **wichtige** Einstellungen vornehmen:
	* **1 System Options:** S3 wählen und neues Passwort vergeben
	* **5 Localisation Options:** L1 wählen und zu `de_DE.UTF-8 UTF-8` scrollen, mit Leertaste auswählen und `ok` bestätigen. Anschließend noch `de_DE.UTF-8` wählen und mit `ok` bestätigen.
	* Konfigurator verlassen und System mit `sudo reboot` den Pi neustarten
	* Wieder über das Terminalprogramm verbinden, mit neuem Passwort einloggen und erneut `sudo raspi-config` ausführen
	* **5 Localisation Options:** L2 wählen und die Zeitzone `Europa` und `Berlin` wählen und mit Enter bestätigen
	* **1 System Options:** S5 Boot / Auto Login mit Enter wählen und B1 Console mit Enter erneut bestätigen.   Mit Tab auf Finish gehen und die Frage nach Reboot mit Ja und Enter bestätigen.

7. Nach dem erneuten einloggen über das Terminalprogramm wird mit dem Einzeiler  
`curl -sLf https://iobroker.net/install.sh | bash - `  
sowohl node.js in der jeweils aktuell empfohlenen Version ***und*** ioBroker installiert.  

Die erfolgreiche ioBroker Installation endet mit der Information unter welcher IP ioBroker aufgerufen werden kann. Unter http://IP-ADRESSE:8081 kann nun ioBroker genutzt werden.


## Installationsablauf ARM-SBC
***noch nicht fertig***
1. Die für die verwendete Hardware passende Version für andere ARM-basierte Einplatinencomputer unter https://www.armbian.com/download/ herunter laden, ***mehr fehlt***
2. Über das Terminalprogramm zum SBC verbinden, indem die IP des SBC unter Port 22 aufgerufen wird und die Zugangsdaten eingeben werden:

	* ***Das fehlt noch***

3. Über dem Aufruf `sudo armbian-config` müssen einige Einstellungen vorgenommen werden.bzw.
    ***Diese Beschreibung fehlt noch***

## Installationsablauf PC
***noch nicht fertig***
1. Das kleine Installations-Image in der 64-Bit Version unter https://www.debian.org/distrib/ herunterladen, entpacken und auf einen Bootfähigen USB-Stick schreiben.
2. Im BIOS noch 
  * den Boot von USB aktivieren 
  * auf ein "Legacy-Betriebssystem" stellen
3. Anschließend vom USB-Stick booten und der geführten Installation folgen und ***keine*** grafische Oberfläche installieren.
4. Sollte in dem System der Zugang mit *root* stattfinden und noch kein normaler User angelegt sein, diesen mit `adduser UserName` (UserName durch den gewünschen Usernamen ersetzen) angelegen und ein Passwort vergeben.  Dem angelegten User noch mit `adduser UserName sudo` noch sudo rechte geben.
5. `curl` installieren
6. usw.
7. ioBroker wird mit dem Befehl `curl -sLf https://iobroker.net/install.sh | bash - ` installiert
Auf einem neuen System, auf dem sich noch kein node.js befindet wird dieses in der jeweils aktuell empfohlenen Version mit installiert.

