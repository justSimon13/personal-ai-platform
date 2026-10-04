# Elena v0.1: lokaler Entscheidungszyklus

## Autorität und Weltzustand

Godot erzeugt einen strukturierten Snapshot mit `schema_version`, `world_revision`, Uhrzeit, Nutzerpräsenz, Bedürfnissen, Emotionen, nahen Objekten und erlaubten Aktionen. Bedürfnisse und Emotionen sind explizite Spielzustände; das Modell verändert sie nicht direkt.

Jede erlaubte Aktion besitzt eine stabile ID, gültige Ziele, Vorbedingungen und Abbruchregeln. Der Snapshot enthält nur den für die lokale Entscheidung nötigen Ausschnitt. Das lokale LLM erhält keine Zugangsdaten und keine Ausführungswerkzeuge.

## Entscheidung und Ausführung

Das Modell liefert ausschließlich eine strukturierte Entscheidung: Snapshot-Revision, erlaubte Aktions-ID, Ziel-ID und begrenzte Priorität. Alternativ liefert es `wait`, `cancel` oder einen Capability Request in einem jeweils definierten Schema. Freitext ist keine ausführbare Anweisung.

Beispiel eines synthetischen Vertrags, noch kein implementiertes API:

```json
{
  "schema_version": 1,
  "world_revision": 42,
  "intent": "act",
  "action_id": "move_to",
  "target_id": "chair_1",
  "priority": 0.6
}
```

Godot prüft Schema, Revision, Aktionsliste, Ziel und aktuelle Vorbedingungen. Es entscheidet über Navigation, Physik, Animation und Ausführung. Die Modellantwort löst niemals direkt Engine-Befehle aus. Bei veraltetem Snapshot erfolgt erneute Validierung bzw. eine neue Entscheidung; eine alte Antwort darf keine neuere Entscheidung überschreiben.

## Abbruch und Umentscheidung

Vorgeschlagener Ablauf: `idle → deciding → validating → executing → completed`; von jeder aktiven Phase aus sind `cancelled` oder `failed` möglich.

Während der Ausführung können relevante Weltänderungen eine neue Entscheidung auslösen. Es gibt maximal eine wirksame Aktion gleichzeitig. Godot bricht die aktuelle Aktion am definierten sicheren Punkt ab, bestätigt den Abbruch und startet erst dann die neue Aktion. Nicht unterbrechbare Abschnitte werden ausdrücklich modelliert. Eine Entscheidungs-ID verhindert, dass verspätete Modellantworten ausgeführt werden.

Ein konfigurierbarer Entscheidungsabstand und eine Prioritätsschwelle begrenzen ständiges Hin-und-her-Wechseln. Konkrete Werte werden anhand des Prototyps gewählt.

## Unbekannte Aktionen und Fehler

Eine nicht erlaubte Aktion wird verworfen. Ein ausdrücklich formulierter Wunsch nach einer neuen Fähigkeit wird lokal als Capability Request gespeichert; Godot führt ihn nicht aus. Anfragen werden dedupliziert bzw. begrenzt, damit ein Modellfehler keine endlose Liste erzeugt.

Bei Timeout, ungültigem JSON, Ollama-Ausfall oder ungültigem Ziel gilt ein deterministischer lokaler Fallback: warten oder die aktuelle Aktion nach Godot-Regeln sicher beenden/abbrechen. Keine automatische Anfrage an externe Modelle. Modellaufrufe erhalten lokale Zeit- und Kontextlimits sowie begrenzte Wiederholungen.

## Modellprüfung auf vorhandener Hardware

Zuerst 4B als Baseline messen: gültige Entscheidungen, falsche Ziele, Abbruchverhalten, Latenz und Speicherbedarf. Danach ein quantisiertes 7–8B-Modell mit derselben synthetischen Szenariofolge prüfen, während Godot die GPU nicht für Rendering nutzt. Modellname, Quantisierung, Kontextlänge und Konfiguration werden lokal festgehalten. Ein größeres Modell wird nur übernommen, wenn es innerhalb vorhandener Ressourcen bessere Ergebnisse liefert.

Modellwechsel, Benchmarks und privates Gedächtnis verbleiben im Elena-Repository. In diesem Repository werden keine privaten Beispielzustände gesammelt.

## Ergänztes v0.1-Ziel aus dem Charter

Die erste Slice ist kleiner als das vollständige v0.1-Ziel. Nach ihr kommen lokaler Textdialog und mindestens fünf semantische Handlungen hinzu: Gespräch beginnen, Sofa nutzen, Sessel nutzen, zur Küche gehen und einfaches Essen zubereiten. TTS bleibt ausgeschlossen. Die im Charter erwähnte vorhandene Godot-3D-Wohnung muss im privaten Repository geprüft werden, bevor ihre Objekte oder Animationen vorausgesetzt werden.

Objekte registrieren Affordances. Fähigkeiten werden versioniert und beschreiben Zieltypen, Parameter, Vorbedingungen, Ausführungslogik sowie Erfolg-, Fehler- und Abbruchereignisse. Godot bestimmt beispielsweise eine tatsächlich freie Sitzposition. Eine vom Modell behauptete Unterbrechbarkeit ist lediglich ein Vorschlag; maßgeblich sind Godots Abbruchregeln.

Ein austauschbarer lokaler Inference-Adapter trennt Modellkonfiguration von Godot. Bei Ressourcenengpässen sind geringerer Kontext, langsamere Ticks oder ein kleineres lokales Modell mögliche explizite lokale Einstellungen. Die im Charter genannten 30–120 Sekunden Simulationszeit sind ein Ausgangspunkt für Messungen, keine festgelegte Echtzeit-Latenz.

### Begrenztes lokales Gedächtnis

Kurzzeitkontext umfasst den letzten Dialog und die aktuelle Aktion. Episoden speichern kompakte Ereignisse; der stabile Weltzustand hält Bedürfnisse, Beziehungen, Gegenstände und Vorhaben. Abruf lädt nur relevante Einträge, kein unkontrolliertes vollständiges Chatlog. Einträge erhalten Quelle, Zeit, Vertrauensgrad und Datenzone `elena_local`. Eine Modellzusammenfassung ist eine abgeleitete Interpretation und überschreibt keine von Godot bestätigten Weltfakten.

Ausführung, Ablehnung und Abbruch werden lokal als Ereignisse gespeichert. Private Dialoge und mögliche Begründungen verbleiben im privaten Bereich und erscheinen nicht in Plattformlogs. Datenbankprodukt, Aufbewahrungsfristen und Abrufverfahren werden erst in der Gedächtnis-Slice bestimmt.

### Abnahme des vollständigen v0.1

Lokaler Textdialog, die fünf Handlungen, validierte Snapshots, Umentscheidung während Bewegung, sichtbare lokale Capability Requests und nachvollziehbare lokale Ereignisse müssen funktionieren. Ein testbarer Netzwerkblock muss externe LLM-Verbindungen verhindern und den lokalen Ollama-Zugriff weiterhin ermöglichen. Diese Abnahme ergänzt die kleinen Slice-Kriterien; sie fordert keinen sofortigen Komplettbau.
