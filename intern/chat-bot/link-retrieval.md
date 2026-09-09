---
title: "Chat-Bot: Link Retrieval"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "chat-bot"
route: "/chat-bot/link-retrieval"
tags: ["chat-bot", "link-retrieval", "knowledge", "directus", "sitemap"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Chat-Bot: Link Retrieval

## Was ist das?

Der Ablauf, um Links einer Kundenwebseite aufzubereiten und als Knowledge in das Backend (Directus) zu importieren.

## Schritte

1. Function in Retell mit richtiger `partnerID` anlegen.
2. Link-Liste aufbereiten.
3. Über Sitemap suchen, meist: `domain/sitemap.xml`.
4. Link-Liste mit AI aufbereiten, mit den Spalten: `data.link`, `partner`, `status`, `description`, `title`.
5. Import der Liste im Backend (Directus) über **Import** in der Collection `knowledge`.

## Ergebnis prüfen

- Links sind in der Collection `knowledge` mit korrekter `partnerID` vorhanden.
- Der Chat-Bot kann passende Links abrufen.