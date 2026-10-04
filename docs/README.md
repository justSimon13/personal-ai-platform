# Konzept und Architektur

Stand: 4. Oktober 2026. Status: Konzept; keine implementierte Laufzeit.

Das Repository war bei der Bestandsaufnahme leer bis auf `.git`; `main` hatte keine Commits. Es gibt keine bestehende Anwendung, Frameworkbindung oder Migration. Die früher genannten Angular-/Event-/JWT-Themen liefern deshalb keine Implementierungsgrundlage für diesen Neuaufbau.

## Lesereihenfolge

1. [Zielbild und Grenzen](01-zielbild.md)
2. [Architektur und gemeinsame Begriffe](02-architektur.md)
3. [Policies, Freigaben und Datengrenzen](03-policy-und-datengrenzen.md)
4. [Elena v0.1](04-elena-v01.md)
5. [Kleine Vertical Slices](05-vertical-slices.md)

Die Dokumente unterscheiden verbindliche Grenzen von vorgeschlagenen technischen Details. Ein Konzept beschreibt noch keine tatsächlich durchgesetzte Sicherheitsgarantie.

## Repository-Schnitt

Jetzt enthält `personal-ai-platform` nur diese Konzepte. Später dürfen hier Jarvis und normale Worker entstehen. Elena erhält ein separates privates Repository; ihr Code, Gedächtnis, Modelle und Daten gehören nicht hierher. Auch Testfixtures hier enthalten keine aus Elena abgeleiteten privaten Daten.

Framework, Datenbankprodukt, Provider-SDK und Worker-Orchestrierung werden erst gewählt, wenn eine kleine Slice ihren konkreten Bedarf zeigt. Es wird weder ein Komplettsystem noch ein universelles Agentenframework vorab gebaut.

## Ergänzende Kontextquellen

Gelesen wurden `oekosystem-architektur.md` und `elena-implementation-charter-v0.1.md` aus dem vom Nutzer genannten lokalen Output-Verzeichnis. Sie dienen als Kontext, nicht als unmittelbarer Umsetzungsauftrag an Claude Code oder einen Worker. Verbindlich bleibt der aktuelle Auftrag: Konzept zuerst, getrennte Repositories und Datenbanken, keine automatische Weitergabe und kein großer Frameworkbau.

Der Kontext ergänzt Elenas v0.1-Ziel um Textdialog, fünf semantische Handlungen und begrenztes lokales Gedächtnis. Eine vorhandene Godot-Wohnung wird dort beschrieben, wurde hier jedoch nicht inspiziert. Die Gateway-Skizze im Ökosystemdokument beschreibt eine spätere Ausbaustufe, keine aktuelle Verbindung. Ein Work Kernel beginnt als Vokabular und Verträge; eine gemeinsame Laufzeit entsteht nicht automatisch.
