---
title: "Retell Voice-Agent-Einrichtung"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/voice-agent"
tags: ["retell", "voice-agent", "llm", "stimme"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Retell Voice-Agent-Einrichtung

## Was ist das?

Die Voice-Agent-Einrichtung in Retell umfasst LLM-Auswahl, Temperatur, Stimme und weitere Basiseinstellungen für eingehende Voice-Agenten.

## Wofür brauchen wir das?

Damit wir Voice-Agenten konsistent und nach Trends4Markets-Standard konfigurieren können.

## Navigation

Retell Workspace → Agent öffnen → Untermenü des Voice-Agenten

Benennung des Voice-Agenten: `Unternehmen-Name Inbound`

In der Agent-Details-Kopfzeile seht ihr Kosten und Token-Schätzung; über den **ID**-Button rechts kopiert ihr die **Agent-ID** (z. B. für den Eintrag in Directus).

![Agent-Details-Kopfzeile mit ID-Button zum Kopieren der Agent-ID](/images/retell/retell-agent-id.png)

![Retell-Agent-Untermenü mit Einstellungsmöglichkeiten](/images/retell/retell-agent-einstellung-untermenü.png)

## Schritte (Retell-Übersicht)

Im Untermenü des Agenten könnt ihr von links nach rechts folgende Einstellungen setzen:

1. Das gewünschte **LLM** auswählen, das der AI-Agent verwenden soll.
2. Die **LLM-Temperature** steuert die Varianz und Konsistenz der Antworten.
3. Im **Stimmen-Menü** zwischen zwei Reitern wählen:
   - **Platform Voices** mit Add voice clone, Gender, Accent
   - **Custom Providers** mit Anbietern (MiniMax, Fish Audio, ElevenLabs, Cartesia, OpenAI), Add custom voice, Gender, Accent, Types, Search

![Auswahl der Agent-Stimme](/images/retell/retell-agent-stimmen-auswahl.png)

## Trends4Markets-Default

| Einstellung | Wert |
| --- | --- |
| LLM | Gemini 3.0 Flash |
| LLM Temperature | 0 |
| Stimme | Anbieter Cartesia (German oder All Types → Custom Providers) |
| Voice Model | Sonic-3.5 |
| Transkriptionsmodul | Deutsch German |
| Agent Handbook | Funktionen alle aus |
| Current timezone | Berlin |

## Ergebnis prüfen

- Agent startet mit korrekter Begrüßung.
- Stimme und Sprache entsprechen dem Kunden-Setup.
- Antworten sind konsistent (Temperature 0).

## Häufige Probleme

| Problem | Lösung |
| --- | --- |
| Inkonsistente Antworten | LLM Temperature prüfen (Default: 0) |
| Falsche Stimme/Sprache | Cartesia \+ German bzw. Custom Provider prüfen |
| Agent reagiert nicht wie erwartet | Agent Handbook-Funktionen prüfen (alle aus) |