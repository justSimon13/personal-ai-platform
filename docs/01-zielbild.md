# Zielbild und Grenzen

## Jarvis

Jarvis ist ein sachlicher Assistent für Organisation, Projekte, Beratung und später Smart Home sowie Worker-Steuerung. Er unterstützt Planung und Entscheidungen. Seine Rolle gewährt keine pauschalen Ausführungsrechte. Jarvis und normale Worker dürfen zunächst externe KI-Anbieter nutzen; übertragene Daten müssen ausdrücklich zum jeweiligen Task freigegeben sein.

## Worker

Ein Worker ist ein zeitlich begrenzter Ausführungsprozess, keine Persönlichkeit. Er erhält genau einen umrissenen Auftrag, explizite Eingaben, ausgewählte Tools, begrenzte Rechte, Kosten-/Zeitlimits und ein erwartetes Ergebnis. Nach Ende des Runs verfallen seine Rechte. Neue Versuche erhalten eine neue Run-ID und eine erneute Prüfung.

Claude Code kann ein Tool eines begrenzten Coding-Workers sein. Seine Nutzung übernimmt die Grenzen dieses Runs; das Tool ist weder Elenas Bewusstsein noch ein Weg, ihre Rechte zu erweitern.

## Elena

Elena ist eine Akteurin in einem vollständig separaten privaten Godot-Projekt. Sie besitzt ein lokales LLM, eine eigene Datenbank und ein eigenes Repository. Gemeinsame technische Begriffe schaffen keine gemeinsame Datenhaltung.

Elena darf Wünsche und Capability Requests formulieren. Sie besitzt keine Shell, keinen Browser, keine Zugangsdaten, kein Git-Push und keine Zahlungszugriffe. Es gibt keinen automatischen Cloud-Fallback. Ein Ausfall des lokalen Modells führt zu lokalem Stillstand bzw. sicherem Godot-Verhalten.

Elena-Code, Gedächtnis und private Daten dürfen niemals automatisch zu Jarvis, externen Modellen oder Workern gelangen. Eine spätere manuelle Übergabe benötigt ein konkret geprüftes, minimiertes Datenpaket; pauschale Einwilligung erzeugt keinen dauerhaften Datenkanal.

## Umfang v0.1

Enthalten: strukturierter Weltzustand, lokale Absichtsentscheidung, erlaubte Aktionen, Godot-Ausführung, Abbruch und Umentscheidung sowie lokal gespeicherte Capability Requests.

Ausgeschlossen: VR, TTS, Browser, externe Dienste, autonomes Coding, Smart Home und Jarvis-Integration. Worker-Anfragen durch Elena sind ein späteres Konzept; v0.1 sendet keine Anfragen an Worker.

## Hardware

Vorläufig läuft Ollama auf dem privaten PC mit RTX 2070 Super und 8 GB VRAM. Ein 4B-Modell dient als funktionierender Prototyp. Ein quantisiertes 7–8B-Modell ist ein lokal zu prüfendes Ziel, wenn die GPU nicht gleichzeitig Godot rendert; Passform, Kontextlänge und Latenz sind nicht garantiert. Jetzt gibt es weder einen neuen KI-PC noch einen Hardwarekauf.
