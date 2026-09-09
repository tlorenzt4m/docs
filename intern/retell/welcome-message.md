---
title: "Retell Welcome Message"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/welcome-message"
tags: ["retell", "welcome-message", "begruessung"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Retell Welcome Message

## Was ist das?

Die Einstellungen zur Begrüßung, die der Agent zu Beginn eines Gesprächs nutzt. Zu finden im Hauptfenster unterhalb des AI-Agent-Promptfensters.

![Einstellungen zur Welcome Message](/images/retell/retell-agent-welcome-message.png)

## Schritte (Retell-Übersicht)

- **Erste Zeile:** Einstellen, ob die Nutzer zuerst sprechen sollen (**User speaks first**) oder der AI-Agent das Gespräch startet (**AI speaks first**).
- **Zweite Zeile:** Einstellen, ob die Welcome Message eine **Custom Message** (eigene Nachricht) oder eine **Dynamic Message** (dynamische Nachricht) sein soll.
- Bei **Custom Message** den gewünschten Text für die Willkommensnachricht eingeben. Der AI-Agent spricht diesen Text zu Beginn der Konversation.
- **Pause before speaking:** Pausenzeit, die der Voice-Agent vor jeder neuen Nachricht wartet.

## Trends4Markets-Default

| Einstellung | Wert |
| --- | --- |
| Welcome Message | **AI speaks first** |
| Custom Message | z. B. „Hallo, ich bin der KI-Assistent für …" |
| Pause before speaking | in der Regel 0,2 |

## Ergebnis prüfen

- Agent startet das Gespräch mit der hinterlegten Begrüßung.
- Pause vor dem Sprechen wirkt natürlich.