# HB-UNI-Sen-CAP-MOIST
## Funk "kapazitiver Bodenfeuchtesensor" für die Integration in HomeMatic

_aktueller Hinweis:<br>
Das eigenständige Addon für den Sensor ist entfallen.
Um die Geräteunterstützung zu aktivieren, wird nun die aktuellste Version des [JP-HB-Devices Addon](https://github.com/jp112sdl/JP-HB-Devices-addon/releases/latest) benötigt! Mit diesem [Addon](https://github.com/jp112sdl/HB-UNI-Sen-CAP-MOIST#addon-installieren) werden alle meine Projekte unterstützt._

#### (mit bis zu 7 Sensoren pro Gerät)

## Verdrahtung
![wiring](Images/wiring2.png)

## benötigte Hardware
* 1x Arduino Pro Mini **ATmega328P (3.3V / 8MHz)**
* 1x CC1101 Funkmodul **(868 MHz)**
* 1x FTDI Adapter (wird nur zum Flashen benötigt)
* 1x Taster (beliebig... irgendwas, das beim Draufdrücken schließt :smiley:)
* 1x LED 
* 1x Widerstand 330 Ohm (R1)
* 1x Widerstand 100k (R2)
* 1x Widerstand 470k (R3)
* 1x ... 7x kapazitiver Feuchtesensor (0...3V Ausgangsspannung) [ebay](https://www.ebay.de/itm/152873639264)
* Draht, um die Komponenten zu verbinden

Um die Batterielebensdauer zu erhöhen, ist es unbedingt notwendig, die grüne LED vom Arduino Pro Mini mit einem kleinen Schraubendreher oder Messer von der Platine zu entfernen!

Die Stromversorgung besteht aus **3x** AA(A)-**Batterien** (oder **4x 1.2V Akkus**).<br>

## Universalplatine
Wer eine eigene Platine herstellen möchte, kann auf eine Auswahl verschiedener vorgefertigter Layouts zurückgreifen.
z.B.:
- [PCB](https://github.com/alexreinert/PCB) von alexreinert
- [HMSensor](https://github.com/pa-pa/HMSensor) von pa-pa

## Code flashen
- [AskSinPP Library](https://github.com/pa-pa/AskSinPP) in der Arduino IDE installieren
  - Achtung: Die Lib benötigt selbst auch noch weitere Bibliotheken, siehe [README](https://github.com/pa-pa/AskSinPP#required-additional-arduino-libraries).
- [Projekt-Datei](https://raw.githubusercontent.com/jp112sdl/HB-UNI-Sen-CAP-MOIST/master/HB-UNI-Sen-CAP-MOIST/HB-UNI-Sen-CAP-MOIST.ino) herunterladen.
- Arduino IDE öffnen
  - Heruntergeladene Projekt-Datei öffnen
  - Werkzeuge
    - Board: Arduino Pro or Pro Mini
    - Prozessor: ATmega328P (3.3V 8MHz) 
    - Port: entsprechend FTDI Adapter
einstellen
- ggf. Anpassungen im Code durchführen (z.B. bei mehreren Sensoren)
- Menü "Sketch" -> "Hochladen" auswählen.

## Addon installieren
Um die Geräteunterstützung zu aktivieren, wird die aktuellste Version des [JP-HB-Devices Addon](https://github.com/jp112sdl/JP-HB-Devices-addon/releases/latest) benötigt!

## Gerät anlernen
Wenn alles korrekt verkabelt und das Addons installiert ist, kann das Gerät angelernt werden.<br>
Über den Button "Gerät anlernen" in der WebUI öffnet sich der Anlerndialog.<br>
Button "HM Gerät anlernen" startet den Anlernmodus.<br>
Nun ist der Taster (an Pin D8) kurz zu drücken.<br>
Die LED leuchtet für einen Moment.<br>
Anschließend ist das Gerät im Posteingang zu finden.<br>
Dort auf "Fertig" geklickt, wird es nun in der Geräteübersicht aufgeführt.<br>
![addon](Images/ccu_geraete.png)
<br><br>
## Kalibrierung
Der [Hersteller des Sensors](https://www.dfrobot.com/wiki/index.php/Capacitive_Soil_Moisture_Sensor_SKU:SEN0193) sieht eine manuelle Kalibrierung vor.<br>
Es müssen die Spannungswerte für beide Feuchte-Grenzen (trocken / nass) ermittelt werden.<br>
Der Wert wird beim Starten des Arduino Pro Mini im seriellen Monitor (57600 Baud) angezeigt.<br>
Siehe `+Sensor   (#n) V:` <br>
![sermon](Images/arduino_ide_serialmonitor.png)

Zur Kalibrierung startet man nun den Arduino Pro Mini ein Mal mit trockenen Sensoren und ein Mal in ein Glas Wasser eingetaucht.
Dabei ergeben sich je Sensor 2 Werte:<br>
<img src="Images/sensor_trocken.png" width=300>&nbsp;<img src="Images/sensor_nass.png" width=300>
<br>
_Der Wert im Trockenen muss höher sein als im Nassen!_

<br><br>
Beide Werte können nun in der WebUI-Gerätekonfiguration eingegeben werden.

## Einstellungen
- Gerät:
  - Low Bat Schwelle
    - ~3.7V
  - Das Sendeintervall kann zwischen 1 und 1440 Minuten eingestellt werden.<br>
- je Kanal:
  - HIGH Value ist der gemessene Analogwert, wenn der Sensor trocken ist.<br>
  - LOW Value ist der gemessene Analogwert, wenn der Sensor komplett nass (in Wasser eingetaucht) ist.<br>

![addon](Images/ccu_einstellungen.png)
<br><br>
## Wert anzeigen
Unter "Status und Bedienung" -> "Geräte" kann der Feuchtigkeitswert angezeigt werden.<br>
Damit man den Datenpunkt auch in Diagrammen verwenden kann, habe ich den systeminternen Datentyp `HUMIDITY` verwendet.
Das hat jedoch einen kleinen Schönheitsfehler zur Folge: Die Bezeichnung lautet "Rel. Luftfeuchte".
Damit kann man wohl leben... :) 
![addon](Images/ccu_status.png)



Eine Verwendung in Programmen ist ebenfalls möglich.


## Beispielaufbau

![aufbau1](Images/aufbau1.jpg)

![aufbau2](Images/aufbau2.jpg)

![aufbau3](Images/aufbau3.jpg)
