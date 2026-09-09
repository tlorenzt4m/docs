---
title: "Retell Agent erstellen"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/agent-erstellung"
tags: ["retell", "agent", "voice-agent", "setup"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Retell Agent erstellen

## Was ist das?

Retell ist eine Plattform zum Erstellen, Testen, Einsetzen und Überwachen von AI-Voice-Agenten für eingehende und ausgehende Anrufe. Sie bietet eine Komplettlösung für konversationelle AI-Agenten, die Telefongespräche natürlich führen, unterstützt eingehende und ausgehende Calls, lässt sich in verschiedene Telefonieanbieter integrieren und bringt Funktionen für Tests und Monitoring mit.

## Wofür brauchen wir das?

Jeder Kunden-Bot beginnt mit einem Retell-Agenten. Dieser Schritt legt fest, welcher Agententyp verwendet wird.

## Navigation

Im Workspace oben rechts auf **Create an Agent** klicken und den gewünschten Agenten auswählen (**Voice Agent** oder **Chat Agent**).

![Retell-Agent-Auswahl](/images/retell/retell-agent-auswahl.png)

## Schritte

Im Fenster **Create agent** den gewünschten Typ wählen:

- **Single prompt:** Leicht zu bedienen, formfreie Konversationen → **nutzen wir**.
- **Conversational flow:** Produktionsfertige, deterministische Konversation.
- **Other options** (oben rechts): Multi-Prompt (Legacy), aktuell nicht genutzt.

![Auswahl des Agent-Typs in Retell](/images/retell/retell-agent-typ-auswahl-2.png)

## Trends4Markets-Default

- Agententyp: **Single prompt**
- Benennung des Voice-Agenten: `Unternehmen-Name Inbound`

## Ergebnis prüfen

- Agent ist im Workspace angelegt und korrekt benannt.
- Folgekonfiguration (LLM, Stimme, Prompt) kann im Agenten-Untermenü erfolgen → siehe [Voice-Agent-Einrichtung](/intern/retell/voice-agent-einrichtung).