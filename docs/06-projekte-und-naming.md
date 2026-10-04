# Projekte, Namen und Repository-Grenzen

Stand: 4. Oktober 2026. Status: Bestandsaufnahme und Namensvorschlag; keine Umbenennung beschlossen oder durchgeführt.

## Geprüfter Bestand

Unter `/Users/simon/Documents/Privat/Apps/personal-ai` liegen zwei getrennte Git-Checkouts:

| Lokaler Ordner | Git-Remote | Aufgabe |
| --- | --- | --- |
| `personal-ai-platform` | `justSimon13/personal-ai-platform` | Plattformkonzept, später Jarvis und begrenzte Worker |
| `Elena-Loft-Assets` | `justSimon13/elena-loft-assets` | Blender-Quellen, Texturen, Asset-Builds, Prüfungen und GLB-/JSON-Exporte |

Das dritte Projekt ist laut Nutzer das noch nicht auf Git befindliche Godot-Game. Es liegt nicht im geprüften Sammelordner; Speicherort, Struktur und Laufzeit wurden nicht verifiziert. GitHub-Inhalte und Repository-Sichtbarkeit wurden nicht geprüft; die Zuordnung stammt aus lokalen Remotes.

Die vorhandenen Plattformdokumente liegen jetzt im verschobenen Checkout. Sie sind zum Prüfzeitpunkt noch untracked und damit nicht über Git synchronisiert.

## Vorgeschlagene Namen

```text
personal-ai/                  lokaler Sammelordner, kein gemeinsames Repository
├── personal-ai-platform/     Plattform: Jarvis und Worker
├── elena-loft-assets/         Asset-Werkstatt, bestehender Repository-Name
└── elena-world/               privates Godot-Projekt, vorgeschlagener Name
```

`personal-ai` bezeichnet das gesamte Ökosystem; `personal-ai-platform` bezeichnet die ausführende Plattform. Die ähnlichen Namen sind sinnvoll, wenn diese Ebenen ausdrücklich dokumentiert sind. Jarvis bleibt ein Produktname innerhalb der Plattform; ein viertes Repository ist derzeit nicht erforderlich.

`elena-world` beschreibt den privaten Charakterraum einschließlich Spiel, lokalem Entscheidungsadapter und Gedächtnis. Es bindet den Namen nicht an die aktuelle Wohnung. `elena-game` wäre verständlich, betont aber vor allem das Spiel. Empfehlung: `elena-world`.

Den bestehenden Namen `elena-loft-assets` jetzt beibehalten. Falls die Werkstatt später mehrere Welten oder allgemeinere Charakter-Assets betreut, kann `elena-assets` erneut bewertet werden. Heute rechtfertigt das keinen Remote-Wechsel. Lokale Projektordner sollten langfristig dieselbe Kleinschreibung mit Bindestrichen wie ihre Repository-Namen verwenden. Bestehende Asset-IDs und Pfadkonventionen bleiben der Asset-Spezifikation unterstellt.

## Zuständigkeiten und Übergabe

| Projekt | Autoritativ für | Gehört nicht hinein |
| --- | --- | --- |
| Plattform | Jarvis, Worker-Runs, Plattform-Policies und übergreifende Vertragskonzepte | Elena-Gedächtnis, private Dialoge, private Laufzeitdaten oder automatisch kopierter Elena-Code |
| Asset-Werkstatt | Asset-Verträge, Blender-Quellen, Exporte und Asset-Validierung | Godot-Runtime, private Dialoge, Gedächtnisdatenbank |
| Elena World | Godot-Szenen, Importer, Interaktionen, lokale Entscheidungen und private Persistenz | Jarvis-Runtime, allgemeine Worker-Steuerung, Cloud-Fallback |

Die Asset-README und `docs/PIPELINE.md` weisen bereits diese Zuständigkeiten aus. `game/assets/world/` im Asset-Repository enthält Exportprodukte; der Ordnername bedeutet nicht, dass dort die Godot-Anwendung lebt.

Übergabe: Asset-Werkstatt → ausgewählte, geprüfte GLB-/JSON-Exporte → Import und In-Engine-Prüfung im privaten Game. Referenz auf Asset-Version bzw. Quell-Commit im Game festhalten. Keine automatische Rücksynchronisation privater Game-Daten. Ein fehlerfreier Blender-Export ist noch kein in Godot geprüftes Asset.

Die README erlaubt auch die Übernahme von `art/`. Für den Runtime-Einstieg werden nur benötigte Exporte übernommen; Blender-Quellen bleiben grundsätzlich in der Werkstatt. Ein Bedarf an zusätzlichem Quellmaterial wird separat begründet. Noch keine Submodule, automatische Synchronisationsdienste oder gemeinsamen Datenbanken einführen.

## Git und private Daten

Ein privates Game-Repository kann später Code und bewusst ausgewählte statische Ressourcen versionieren. Gedächtnisdatenbank, Gespräche, Secrets, lokale Logs und Modellgewichte bleiben außerhalb versionierter Inhalte. Ein privates Remote allein ersetzt diese Trennung nicht. Bevor das Game zu GitHub übertragen wird, muss ausdrücklich entschieden werden, welche Code- und Asset-Inhalte hochgeladen werden dürfen; das folgt nicht aus der Existenz der beiden anderen Remotes.

Das Asset-Repository enthält bereits charakterbezogene Spezifikationen. Diese Zugehörigkeit erlaubt keinen Export von privatem Elena-Gedächtnis oder Dialogen. Künftige Asset-Aufträge erhalten nur gezielt freigegebene Produktionsanforderungen.

## Kleine nächste Schritte

1. Projektbezeichnungen und den tatsächlichen Speicherort des Games festhalten.
2. Im Game lokale Ordner für Runtime-Code, importierte Assets und nicht versionierte private Daten prüfen; erst dann einen konkreten Git-Vorschlag erstellen.
3. Einen einzigen Asset-Import samt Quellversion und Godot-Prüfung dokumentieren.
4. Erst darauf den lokalen Entscheidungszyklus aus E1 aufsetzen.

Diese Schritte ändern keine Repository-Grenzen und setzen keine Worker- oder Jarvis-Verbindung voraus.
