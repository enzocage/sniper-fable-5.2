# Cold Meridian

**Gebäude:** 20 Bautypen im Marskolonie-Stil (Kuppel, Zelt-Tonne, Zikkurat, Trommelturm, Doppelkuppel, Pilz, Radar-Hab, Gewächshaus, Spire, Silo-Gruppe, Hangar, Pyramide, Untertasse, gerippte Kuppel, Würfel-Labor, Röhren-Knoten, Terrassenkugel, Segeldach, Trommel mit Kegel, Himmelskapseln) in allen Größen und mit 1 bis 4 Stockwerken, verteilt auf alle Karten.

**Setting:** eine Marskolonie. Rostrote Wüste mit Mondkratern in allen Größen (von wenigen Metern bis über 100 m), Felsbrocken statt Bäumen, weiße Kolonie-Module mit Kuppeln, Antennen, Solarfeldern und Lichtleisten, keine Vögel. Du bist der einzige Mensch, alle Gegner sind Roboter.

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
| Rechtsklick / `F` | Zielfernrohr, Mausrad ändert die Vergrößerung (4× bis 20×, mit Optik bis 32×) |
| `Shift` (im Zielfernrohr) | Luft anhalten: ruhiger zielen, Zeit läuft langsamer |
| `Q` / `E` | Absehen-Einstellung (Nullpunkt) in 50-m-Schritten |
| `1` `2` `3` | Standard-, panzerbrechende, Lockmunition |
| `C` `X` `Leertaste` | Hocken, Liegen, Aufstehen; `Leertaste` im Stehen springt (ca. 1,3 m) |
| Linksklick / `R` | Schießen / Nachladen |
| `T` | Aufklärungsdrohne mit Videobild (ca. 1 Minute Akku, lädt in unter einer Minute nach): `W A S D` fliegen, `Q` hoch, `E` runter, `Shift` schneller, Maus schaut, Klick markiert die Einheit im Bild. Zu nahe an Einheiten lösen Alarm aus. |
| `J` | Orbitallaser: Satellitenansicht, Mausrad zoomt bis auf Straßenhöhe, Ziehen/`W A S D` verschiebt, Klick setzt das Kreuz, `Enter` feuert. Einmal pro Auftrag, mindestens 280 m von dir entfernt. Vernichtet alles im Umkreis von ca. 210 m (Pilzwolke, Druckwelle, Krater bleibt). |
| `N` | Kamera-Rakete: `N` schärft, Linksklick startet (einmal pro Auftrag). Lenken mit Maus oder `A D`, `Q E` Neigung, `W S` Tempo. Das Kamerabild rauscht und verliert mit der Entfernung das Signal. Einschlag zerstört Gebäude im Umkreis von 30 m und zerstört Einheiten im Umkreis von 45 m. |
| `L` | Scheinwerfer des Jeeps (standardmäßig aus; im Dunkeln oder Nebel ist der Jeep ohne Licht kaum zu sehen) |
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

## Schwierigkeit und Taktik

Auf dem Startbildschirm gibt es drei Stufen: **Recruit** (langsamere Entdeckung, kleinere Garnison, Gegner treffen schlechter, Honorar ×0,8), **Veteran** (das vorgesehene Spiel) und **Ghost** (schärfere Sicht, größere Garnison, ein zusätzlicher versteckter Scharfschütze, schnellere Verstärkung, keine Einschlagsanzeige, Honorar ×1,45). Auf allen Karten laufen zusätzliche Perimeter-Patrouillen, die deine Anmarschwege kreuzen. Büsche und Hecken verdecken und dämpfen Sichtlinien (hocken oder liegen in einem Busch wirkt stark). Die Exposure-Anzeige hat einen Ton: ein dunkles Dröhnen, das exponentiell lauter wird, je näher du 100 % kommst.

## Spielprinzip

* **Ballistik:** Geschosse haben Flugzeit, Luftwiderstand, Fall und Winddrift. Entfernung messen, Nullpunkt wählen, mit dem Mil-Absehen vorhalten.
* **Tarnung:** Lärm, Wracks, Sichtlinie und Haltung füllen die Entdeckungsanzeige. Donner, Kirchenglocke und Schiffshorn überdecken einen Schuss; mit Schalldämpfer ist man nur im Umkreis hörbar. Sirenen und Generatoren lassen sich ausschalten.
* **Aufträge:** mehrere Ziele pro Auftrag, Reihenfolge-Abhängigkeiten, Fahrzeuge, Zeitlimits, optionale Zusatzziele und Boni. Zivilisten kosten Geld.
* **Gegner-KI:** Gegner suchen Deckung, rücken von Deckung zu Deckung vor, lugen aus der Deckung, flankieren, funken sich Hinweise zu (Reichweite sinkt, wenn das Relais zerstört ist) und durchsuchen die letzte bekannte Position. Beim Aufspüren einer Wrack oder eines Schusses verstecken sich Wachen, statt zu stürmen.
* **Versteckte Scharfschützen:** getarnte Schützen liegen im Gelände. Ein Schuss von ihnen erscheint als roter Punkt auf dem Kompass; nach einem Schuss wechseln sie die Stellung.
* **Fahrzeuge:** eigener Jeep (befahrbar, überfährt Gegner), Patrouillenfahrzeuge der Gegner, die bei Alarm absitzen, und ein Verstärkungs-Lkw nach einem Sirenenalarm.
* **Roboter:** Außer dir ist niemand ein Mensch. Wachen, Offiziere, Scharfschützen und unbewaffnete Serviceroboter sind humanoide Maschinen im Look des AgiBot A3 (weiße Schale, glänzender schwarzer Kopf und Gelenke); sie unterscheiden sich nur in Farben (Trooper, Scout, Heavy, Kommandoeinheit, Tarn-Scharfschütze). Ein Statuslicht an Kopf und Hals zeigt den Zustand: Cyan/Grün ruhig, Amber misstrauisch, Rot im Kampf.
* **Sichtfeld und Waffenreichweite:** Jede Einheit hat ein Sichtfeld, eine Sichtweite und eine Schussreichweite (Trooper 110°/115 m/135 m, Scout 130°/140 m/110 m, Heavy 90°/105 m/160 m, Scharfschützen 50°/420–480 m/520 m). Auf Abschüsse reagieren nur Einheiten, die sie sehen konnten (Sichtfeld, Reichweite, freie Sicht). Geschossen wird nur innerhalb der Waffenreichweite, außerhalb rücken die Einheiten vor. Auf der taktischen Karte zeigt ein Keil das Sichtfeld.
* **Figuren (Technik):** Jede Person ist ein Skinned Mesh mit 15 Knochen und zufälligem Aussehen (Helm, Mütze, Weste, Rucksack, Brille, Mantel, Ghillie). Arme und Beine nutzen Zwei-Knochen-IK: Hände folgen den Waffengriffen, Schritte folgen der gelaufenen Strecke. Wachen schlendern mit wechselndem Tempo, rauchen, funken, strecken sich, unterhalten sich zu zweit und blicken sich um; Zivilisten fliehen oder kauern.
* **Welt:** begehbare Häuser mit Treppen, Leitern, Balkonen und Dächern; Wasser, Wetter, Tag und Nacht.
* **Ausrüstung:** Nach jedem Auftrag lassen sich Schalldämpfer, Zielfernrohr, Schaft und Munitionstasche kaufen. Der Spielstand liegt im `localStorage` des Browsers.

## Karten und Aufträge

| Karte | Aufträge |
| --- | --- |
| Karvel Basin (Söldnerhof im Hochland) | Ledger, Dead Air |
| Sankt Varga (Dorf am Fluss, Burgruine) | Vespers, House Call |
| Grimsvik Harbour (Frachthafen, Klippen) | Dry Dock, Lantern |
| Altheim Pass (Schnee, Bahnlinie, Kloster) | Last Carriage (fahrender Zug), Cloister (Schneesturm, Seilbahn), Whiteout (Blizzard mit Nebel, unter 100 m Sicht) |

Zwei zusätzliche Marsbasen mit je zwei Aufträgen: Olympus Rim (Kolonie in einem Riesenkrater: Rim Station, Dust Relay) und Valles Station (Canyon-Kolonie um einen Eiskanal: Canyon Broker, Blackout Dome), mit Solarfeldern, Landeplätzen samt Shuttle, Wohnmodulen und Radarfeldern.

Dazu fünf Nacht- und Winter-Varianten auf denselben Karten: Blackout (sternenlose Nacht, Karvel), Winter Bell (Schneetag, Sankt Varga), Pale Harbour (Winternebel, Grimsvik), Long Night (Nachtblizzard, Grimsvik) und Whiteout (Altheim). Alle 17 Aufträge haben Vorschaubilder auf dem Startbildschirm.

## Karte und Hilfe

`Tab` öffnet die Übersichtskarte: Höhenlinien, Raster, Benennungen, berechnete Schussplätze (V1, V2) mit Reichweite, deckungsorientierte Schleichroute, Aufklärungszonen der Ziele und Strategietipps. Die Karte zeigt das gesamte Gelände samt Umgebung; das Missionsgebiet ist gestrichelt umrandet. Mausrad zoomt, Ziehen verschiebt, Klick setzt einen Wegpunkt. `H` öffnet das Feldhandbuch (steht auch auf dem Startbildschirm).

## Radio

`O` öffnet einen kleinen Musikplayer (Wiedergabe, Vor/Zurück, Zufall, Suchleiste, Titelliste). Mit **＋** (oder per Drag & Drop auf den Player) fügst du eigene MP3-Dateien hinzu; sie bleiben auf diesem Gerät gespeichert und spielen überall. Zusätzlich liegt die Spheric-Lounge-Playlist von enzocage.de als Stream bereit; das funktioniert nur, wo der Viewer externe Medien erlaubt (zum Beispiel in der lokal geöffneten Datei, nicht in der Artefakt-Vorschau). Zwei Regler stellen Musik- und FX-Lautstärke getrennt ein (Standard 20 % Musik, 80 % FX). Zu Beginn jedes Auftrags startet automatisch ein zufälliger Titel (nach manuellem Pausieren nicht mehr). Auf dem Handy öffnet die Taste ♪ oben in der Mitte den Player.

## Technik

* Three.js r128, WebGL, eigene Himmels- und Wasser-Shader.
* Höhenfeld-Gelände: Sicht, Kollision und Ballistik nutzen dieselbe Höhenfunktion.
* Gebäude werden prozedural aus Wänden mit Fenster- und Türöffnungen, Stockwerken und Treppen zusammengesetzt und als ein Mesh gebündelt.
* Der gesamte Ton wird beim ersten Start einmal in Sample-Puffer gerechnet (geschichtetes Rauschen, gedämpfte Resonanzen, Formantstimmen) und dann mit Laufzeitverzögerung, Luftdämpfung, Panning und Hall pro Karte abgespielt.

## Dateien

* `cold-meridian.html`: das gesamte Spiel
* `README.md`: diese Datei
