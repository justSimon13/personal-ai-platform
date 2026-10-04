# Policies, Freigaben und Datengrenzen

## Durchsetzung

Modelltexte, Toolausgaben und importierte Artefakte sind untrusted data. Sie dürfen Policies, Approvals oder Capabilities nicht ändern. Durchsetzung liegt beim Runner bzw. in Elenas Fall bei Godot und dem lokalen Adapter; Promptanweisungen allein sind keine Zugriffskontrolle.

Standard ist Ablehnung: Eine nicht ausdrücklich zugewiesene Operation oder Ressource ist nicht zugänglich. Worker besitzen weder Dauerrechte noch automatisch geerbte Nutzerrechte. Tooladapter und Prozessisolation müssen dieselben Grenzen durchsetzen; insbesondere ein Coding-Tool darf über Unterprozesse, Netzwerk oder eingebettete Tools keine Rechte umgehen.

## Datenbereiche

| Bereich | Zulässiger Zugriff |
| --- | --- |
| Jarvis | Jarvis und aufgabenbezogen explizit freigegebene Worker-Eingaben |
| Worker-Run | Eigene Eingaben, freigegebene Ressourcen und eigene Artefakte bis zur vorgesehenen Aufbewahrung |
| Elena privat | Nur Elenas lokale Komponenten; kein automatischer Export |
| Manuelles Übergabepaket | Nur konkret vom Nutzer geprüfte Felder und ausdrücklich bestimmte Empfänger |

Private Elena-Pfade werden nie in normale Worker-Workspaces eingebunden. Es gibt keine automatischen Backups, Telemetrie, Promptlogs oder Fehlerberichte in externe Dienste aus dem Elena-Bereich. Ollama wird lokal verwendet; seine Erreichbarkeit und ausgehende Verbindungen sind beim späteren lokalen Setup zu prüfen. Gemeinsame Hardware ersetzt keine logische oder technische Trennung.

## Konkrete Approvals

Eine Freigabe bindet Empfänger, Zweck, Operation, Ressourcen, Eingabeversion bzw. Hash, Datenumfang, Ablaufzeit und Zahl erlaubter Nutzungen. Jede wesentliche Änderung macht sie ungültig. Freigaben sind widerrufbar; ein Widerruf verhindert weitere Schritte und löst einen Abbruch aus. Bereits ausgeführte Seiteneffekte bleiben im lokalen Audit sichtbar.

Ein Approval kann Verbote einer Policy nicht stillschweigend überschreiben. Eine neue Fähigkeit benötigt zusätzlich eine ausdrückliche Policy-/Capability-Änderung.

## Capability Request

Vorgeschlagene Felder: ID, Ursprung, gewünschte Fähigkeit, Zweck, lokale sichere Alternative, benötigte Ressourcen, erwartete Datenfreigabe und Status. Private Begründungen bleiben lokal. Für externe Vorbereitung erstellt der Nutzer später ein separates, minimiertes Übergabepaket; der vollständige Request wird nicht automatisch exportiert.

Späterer Ablauf:

1. Elena speichert den Wunsch lokal, ohne ihn auszuführen.
2. Der Nutzer prüft die gewünschte Erweiterung und ihren konkreten Umfang.
3. Erst nach Freigabe darf ein begrenzter Worker ein geprüftes Paket zur Vorbereitung erhalten.
4. Der Worker liefert einen Vorschlag bzw. ein Artefakt; er installiert keine Rechte in Elena.
5. Der Nutzer prüft Integration und Aktivierung separat im privaten Projekt.

Freigabe zur Vorbereitung ist keine Freigabe zur Aktivierung. v0.1 endet nach Schritt 1 und bietet lokale Sichtung durch den Nutzer.

## Spätere Nachweise

Vor echter Ausführung sind negative Prüfungen nötig: Zugriff auf Elena-Pfade, unzulässige Tools, abgelaufene oder veränderte Approvals, Cloud-Fallback und Budgetüberschreitungen müssen abgewiesen werden. Logs enthalten nur notwendige Metadaten und verbleiben im jeweiligen Datenbereich; Prompt- und Gedächtnisinhalt werden nicht pauschal protokolliert.

## Spätere zusätzliche Zonen

Der Kontext unterscheidet außerdem Öffentlich/Gast, Arbeit, Venture und Private Vault. Diese werden bei entsprechenden Jarvis-Aufträgen als getrennte Zonen mit eigenen Identitäten, Ressourcen und Freigaberegeln konkretisiert. Gastzugriff erhält keine persönliche Historie; Arbeit und Venture bleiben von Privat getrennt; Bank-, Gesundheits-, Steuer- und Vertragsdaten benötigen einen separaten geschützten Speicher und besonders enge Rechte. Das Konzept erteilt dafür noch keinen Zugriff.

Ein späterer Capability Gateway verwendet getrennte Service-Identitäten und überprüft Quelle, Sitzung, Zielressource und Policy. Dass zwei Akteure dieselbe Operation kennen, gewährt weder gemeinsame Rechte noch gegenseitigen Datenzugriff. Der Gateway ist außerhalb von Elena v0.1.
