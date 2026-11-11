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
| `G` | Jeep einsteigen / aussteigen (Fahren: `W A S D`, `Leertaste` bremst, `Shift` Boost) |
| `Tab` / `M` | Übersichtskarte (zoombar, mit Namen, Schussplätzen und Routen) |
| `B` | Verbandspäckchen |
| `H` / `F1` | Hilfe (Feldhandbuch) |
| `O` | Radio: Musikplayer als Mini-Overlay mit eigenen Reglern für Musik und FX (pausiert das Spiel, solange er offen ist) |
| `Esc` | Pause |

### Touch-Steuerung (Handy/Tablet, Querformat)

Wird automatisch erkannt. Fast unsichtbar: Tasten sind nur schwach eingeblendet.

* **Links irgendwo wischen:** schwebender Joystick (Ring erscheint unter dem Daumen). Weit über den Ring hinaus ziehen = Sprint.
* **Rechts wischen:** umsehen (schnelle Wischer werden leicht beschleunigt). **Doppeltippen:** Zielfernrohr.
* **Großer Ring unten rechts:** Schuss. Der Daumen darf darauf liegen bleiben und weiter zielen.
* **Weitere Tasten:** Zielfernrohr, Nachladen, Haltung (Stehen/Hocken/Liegen), Jeep, Munition, Verband; im Zielfernrohr Luft anhalten, Zoom ±, Absehen ±; im Fahrzeug Bremse. Oben mittig: Karte, Hilfe, Pause.
* Karte: Pinch zum Zoomen, ein Finger verschiebt. Vollbild und Querformat werden beim ersten Tippen angefordert. Zum Testen am Desktop: `?touch` an die URL hängen.

## Spielprinzip

* **Ballistik:** Geschosse haben Flugzeit, Luftwiderstand, Fall und Winddrift. Entfernung messen, Nullpunkt wählen, mit dem Mil-Absehen vorhalten.
* **Tarnung:** Lärm, Leichen, Sichtlinie und Haltung füllen die Entdeckungsanzeige. Donner, Kirchenglocke und Schiffshorn überdecken einen Schuss; mit Schalldämpfer ist man nur im Umkreis hörbar. Sirenen und Generatoren lassen sich ausschalten.
* **Aufträge:** mehrere Ziele pro Auftrag, Reihenfolge-Abhängigkeiten, Fahrzeuge, Zeitlimits, optionale Zusatzziele und Boni. Zivilisten kosten Geld.
* **Gegner-KI:** Gegner suchen Deckung, rücken von Deckung zu Deckung vor, lugen aus der Deckung, flankieren, funken sich Hinweise zu (Reichweite sinkt, wenn das Relais zerstört ist) und durchsuchen die letzte bekannte Position. Beim Aufspüren einer Leiche oder eines Schusses verstecken sich Wachen, statt zu stürmen.
* **Versteckte Scharfschützen:** getarnte Schützen liegen im Gelände. Ein Schuss von ihnen erscheint als roter Punkt auf dem Kompass; nach einem Schuss wechseln sie die Stellung.
* **Fahrzeuge:** eigener Jeep (befahrbar, überfährt Gegner), Patrouillenfahrzeuge der Gegner, die bei Alarm absitzen, und ein Verstärkungs-Lkw nach einem Sirenenalarm.
* **Figuren:** Jede Person ist ein Skinned Mesh mit 15 Knochen und zufälligem Aussehen (Helm, Mütze, Weste, Rucksack, Brille, Mantel, Ghillie). Arme und Beine nutzen Zwei-Knochen-IK: Hände folgen den Waffengriffen, Schritte folgen der gelaufenen Strecke. Wachen schlendern mit wechselndem Tempo, rauchen, funken, strecken sich, unterhalten sich zu zweit und blicken sich um; Zivilisten fliehen oder kauern.
* **Welt:** begehbare Häuser mit Treppen, Leitern, Balkonen und Dächern; Wasser, Wetter, Tag und Nacht.
* **Ausrüstung:** Nach jedem Auftrag lassen sich Schalldämpfer, Zielfernrohr, Schaft und Munitionstasche kaufen. Der Spielstand liegt im `localStorage` des Browsers.

## Karten und Aufträge

| Karte | Aufträge |
| --- | --- |
| Karvel Basin (Söldnerhof im Hochland) | Ledger, Dead Air |
| Sankt Varga (Dorf am Fluss, Burgruine) | Vespers, House Call |
| Grimsvik Harbour (Frachthafen, Klippen) | Dry Dock, Lantern |
| Altheim Pass (Schnee, Bahnlinie, Kloster) | Last Carriage (fahrender Zug), Cloister (Schneesturm, Seilbahn) |

## Karte und Hilfe

`Tab` öffnet die Übersichtskarte: Höhenlinien, Raster, Benennungen, berechnete Schussplätze (V1, V2) mit Reichweite, deckungsorientierte Schleichroute, Aufklärungszonen der Ziele und Strategietipps. Die Karte zeigt das gesamte Gelände samt Umgebung; das Missionsgebiet ist gestrichelt umrandet. Mausrad zoomt, Ziehen verschiebt, Klick setzt einen Wegpunkt. `H` öffnet das Feldhandbuch (steht auch auf dem Startbildschirm).

## Radio

`O` öffnet einen kleinen Musikplayer (Wiedergabe, Vor/Zurück, Zufall, Suchleiste, Titelliste) mit den Spheric-Lounge-Tracks, die per Stream von enzocage.de geladen werden (Internet nötig). Falls der Stream blockiert ist (zum Beispiel in der Artefakt-Vorschau, die fremde Medien-Server sperrt), schaltet der Player automatisch auf einen eingebauten, generativen Ambient-Kanal um, der ohne Netz läuft. Zwei Regler stellen Musik- und FX-Lautstärke getrennt ein; beide werden gespeichert. Auf dem Handy öffnet die Taste ♪ oben in der Mitte den Player.

## Technik

* Three.js r128, WebGL, eigene Himmels- und Wasser-Shader.
* Höhenfeld-Gelände: Sicht, Kollision und Ballistik nutzen dieselbe Höhenfunktion.
* Gebäude werden prozedural aus Wänden mit Fenster- und Türöffnungen, Stockwerken und Treppen zusammengesetzt und als ein Mesh gebündelt.
* Der gesamte Ton wird beim ersten Start einmal in Sample-Puffer gerechnet (geschichtetes Rauschen, gedämpfte Resonanzen, Formantstimmen) und dann mit Laufzeitverzögerung, Luftdämpfung, Panning und Hall pro Karte abgespielt.

## Dateien

* `cold-meridian.html`: das gesamte Spiel
* `README.md`: diese Datei
