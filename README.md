# Cold Meridian

Ein 3D-Scharfschützenspiel für den Browser, in einer einzigen HTML-Datei (`cold-meridian.html`). Kein Build, keine Assets: Gelände, Gebäude, Figuren und der komplette Ton werden beim Start im Browser erzeugt. Das Spiel ist von Spielen wie *Sniper Ghost Warrior Contracts* inspiriert, aber eigenständig (eigene Welt, Figuren, Aufträge).

## Starten

Die Datei in einem aktuellen Desktop-Browser öffnen (Chrome, Edge, Firefox). Three.js wird beim Laden von cdnjs bezogen, deshalb ist eine Internetverbindung nötig. Gespielt wird mit Tastatur und Maus; der Ton startet erst, wenn man einen Auftrag beginnt.

Optional lokal ausliefern:

```bash
python3 -m http.server 8000
```

Dann `http://localhost:8000/cold-meridian.html` öffnen.

## Steuerung

| Taste | Aktion |
| --- | --- |
| `W A S D` | Bewegen, `Shift` sprintet (an Leitern: `W` hoch, `S` runter) |
| Rechtsklick / `F` | Zielfernrohr, Mausrad ändert die Vergrößerung |
| `Shift` (im Zielfernrohr) | Luft anhalten: ruhiger zielen, Zeit läuft langsamer |
| `Q` / `E` | Absehen-Einstellung (Nullpunkt) in 50-m-Schritten |
| `1` `2` `3` | Standard-, panzerbrechende, Lockmunition |
| `C` `X` `Leertaste` | Hocken, Liegen, Aufstehen |
| Linksklick / `R` | Schießen / Nachladen |
| `Tab` / `M` | Taktische Karte |
| `B` | Verbandspäckchen |
| `H` / `F1` | Hilfe (Feldhandbuch) |
| `Esc` | Pause |

## Spielprinzip

* **Ballistik:** Geschosse haben Flugzeit, Luftwiderstand, Fall und Winddrift. Entfernung messen, Nullpunkt wählen, mit dem Mil-Absehen vorhalten.
* **Tarnung:** Lärm, Leichen, Sichtlinie und Haltung füllen die Entdeckungsanzeige. Donner, Kirchenglocke und Schiffshorn überdecken einen Schuss; mit Schalldämpfer ist man nur im Umkreis hörbar. Sirenen und Generatoren lassen sich ausschalten.
* **Aufträge:** mehrere Ziele pro Auftrag, Reihenfolge-Abhängigkeiten, Fahrzeuge, Zeitlimits, optionale Zusatzziele und Boni. Zivilisten kosten Geld.
* **Welt:** begehbare Häuser mit Treppen, Leitern, Balkonen und Dächern; Wasser, Wetter, Tag und Nacht.
* **Ausrüstung:** Nach jedem Auftrag lassen sich Schalldämpfer, Zielfernrohr, Schaft und Munitionstasche kaufen. Der Spielstand liegt im `localStorage` des Browsers.

## Karten und Aufträge

| Karte | Aufträge |
| --- | --- |
| Karvel Basin (Söldnerhof im Hochland) | Ledger, Dead Air |
| Sankt Varga (Dorf am Fluss, Burgruine) | Vespers, House Call |
| Grimsvik Harbour (Frachthafen, Klippen) | Dry Dock, Lantern |

## Technik

* Three.js r128, WebGL, eigene Himmels- und Wasser-Shader.
* Höhenfeld-Gelände: Sicht, Kollision und Ballistik nutzen dieselbe Höhenfunktion.
* Gebäude werden prozedural aus Wänden mit Fenster- und Türöffnungen, Stockwerken und Treppen zusammengesetzt und als ein Mesh gebündelt.
* Der gesamte Ton wird beim ersten Start einmal in Sample-Puffer gerechnet (geschichtetes Rauschen, gedämpfte Resonanzen, Formantstimmen) und dann mit Laufzeitverzögerung, Luftdämpfung, Panning und Hall pro Karte abgespielt.

## Dateien

* `cold-meridian.html`: das gesamte Spiel
* `README.md`: diese Datei
