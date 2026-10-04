# Umsetzung in kleinen Vertical Slices

Jede Slice liefert einen überprüfbaren Ende-zu-Ende-Ablauf. Umsetzung beginnt erst in einem folgenden Arbeitsauftrag; dieses Dokument legt keine Frameworkwahl fest. Elena-Slices werden ausschließlich im eigenen privaten Repository umgesetzt.

## E1 — Eine lokale Entscheidung

Godot-Szene mit einem synthetischen Objekt, `wait` und `move_to`; strukturierter Snapshot → lokales 4B-Modell → Validator → sichtbar ausgeführte Aktion. Noch kein privates Langzeitgedächtnis.

Abnahme: erlaubtes Ziel funktioniert; unbekannte Aktion, ungültiges JSON und veraltete Antwort werden abgewiesen; Ollama-Ausfall führt zu lokalem sicheren Verhalten. Kein externer Modellaufruf.

## E2 — Unterwegs umentscheiden

Während einer Bewegung ändert sich ein relevantes Weltmerkmal. Elena entscheidet neu, Godot bestätigt den sicheren Abbruch und beginnt die neue Aktion.

Abnahme: maximal eine aktive Aktion; verspätete Antworten starten nichts; nicht unterbrechbare Abschnitte werden berücksichtigt; die Szene pendelt nicht fortwährend zwischen Zielen.

## E3 — Fehlende Fähigkeit wünschen

Ein Wunsch nach einer nicht vorhandenen Aktion erzeugt einen lokal persistierten Capability Request mit einfacher lokaler Sichtung.

Abnahme: keine Ausführung, kein Workerstart, kein Export; Wiederholungen werden begrenzt. Nutzer kann den Request lokal ablehnen oder zur späteren Prüfung markieren, ohne dadurch eine Fähigkeit zu aktivieren.

## E4 — Lokaler Textdialog und fünf Handlungen

Die lokal geprüfte Godot-Wohnung erhält Textdialog sowie Sofa-, Sessel-, Küchen- und einfache Essensaktionen. Objekt-Affordances bestimmen gültige Ziele und freie Interaktionspositionen. Aufbau erfolgt Handlung für Handlung auf dem Validator aus E1.

Abnahme: alle fünf semantischen Handlungen sind wählbar und geprüft; ungültige oder belegte Ziele werden abgelehnt; Gespräch gibt keine zusätzlichen Rechte. Kein TTS und keine externen Dienste.

## E5 — Begrenztes Gedächtnis und Abschluss v0.1

Ein bestätigtes Ereignis wird lokal gespeichert und für eine spätere passende Entscheidung gezielt abgerufen. Bedürfnisse und Emotionen entwickeln sich durch definierte Welt- und Gesprächsereignisse; Modelltext verändert sie nicht direkt.

Abnahme: Einträge besitzen Quelle, Zeit, Vertrauensgrad und Datenzone; Abruf ist begrenzt; Modellinterpretationen bleiben von Weltfakten unterscheidbar. Die vollständigen v0.1-Kriterien aus dem Elena-Dokument werden geprüft, einschließlich Netzwerkblock und lokalem Event-Log.

## J1 — Jarvis organisiert einen Task

Hier im Plattform-Repository: Nutzerauftrag → strukturierter Task und Plan → sichtbare Prüfung. Ein externer KI-Anbieter darf mit explizit vorgesehenen Taskdaten arbeiten. Noch keine Tools mit Seiteneffekten.

Abnahme: Plan ist versioniert; Inputs sind nachvollziehbar; Elena-Pfade und -Inhalte sind nicht verfügbar. Ein Providerfehler bleibt ein sichtbarer Taskfehler.

## W1 — Begrenzter Worker liefert ein Artefakt

Ein explizit gestarteter Worker bearbeitet synthetische Daten mit einem ungefährlichen Tool im eigenen Workspace und erzeugt ein Artefakt. Zeit-, Kosten- und Toolgrenzen sowie Abbruch werden vor realen Integrationen geprüft.

Abnahme: unerlaubte Ressourcen und Tools werden abgelehnt; Budgetende stoppt den Run; das Artefakt besitzt Herkunft und Datenbereich; Rechte verfallen nach Runende. Kein Zugriff auf Elena.

## W2 — Konkrete Freigabe vor Seiteneffekt

Ein simulierter Schreibvorgang wartet auf eine an Eingaben und Operation gebundene Freigabe.

Abnahme: Ablehnung, Widerruf, Ablauf und geänderte Eingaben verhindern den Vorgang; dieselbe einmalige Freigabe lässt sich nicht erneut verwenden. Erst danach wird ein echter Integrationsbedarf bewertet.

## Später, außerhalb v0.1

Capability-Vorbereitung durch einen Coding-Worker ist eine separate Slice: manuell geprüftes Übergabepaket → begrenzter Worker → prüfbares Artefakt → separate private Integration. Claude Code wird erst dann als Tool bewertet, einschließlich seiner tatsächlich durchsetzbaren Prozess- und Netzwerkgrenzen.

Smart Home, Jarvis-Elena-Verbindung, TTS und VR brauchen jeweils einen neuen Auftrag und eigene Abnahmekriterien.

## Entscheidungen vor der jeweiligen Slice

Für E1: Elena-Repository und Godot-Version bestimmen, vorhandenes 4B-Modell benennen, lokale Adapter-Schnittstelle und Timeouts wählen. Für J1: erster konkreter Organisationsfall, externe Datenfreigabe und Anbieter wählen. Für W1: Runner-Isolation, ein Tool und messbare Limits bestimmen. Diese Entscheidungen blockieren die Konzepterstellung nicht und rechtfertigen keinen Komplettbau.
