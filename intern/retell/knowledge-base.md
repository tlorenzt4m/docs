---
title: "Retell Knowledge Base"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/knowledge-base"
tags: ["retell", "knowledge-base", "rag", "wissensdatenbank"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Retell Knowledge Base

## Was ist das?

Wissensdatenbanken sind Sammlungen von Informationsquellen, auf die der Agent während eines Anrufs zugreift, um relevante Informationen abzurufen und der Konversation zusätzlichen Kontext zu geben. Das verbessert die Antwortqualität – besonders bei vielen Informationen, die für den Prompt zu umfangreich sind. Ideal für Support-, Helpdesk- und FAQ-Anwendungsfälle.

Unterstützte Inhalte:

- **Website-Inhalte** (über URLs)
- **Dokumente:** .bmp, .csv, .doc, .docx, .eml, .epub, .heic, .html, .jpeg, .png, .md, .msg, .odt, .org, .p7s, .pdf, .ppt, .pptx, .rst, .rtf, .tiff, .txt, .tsv, .xls, .xlsx, .xml
- **Benutzerdefinierte Textausschnitte**

## Wie funktioniert die Knowledge Base?

Wissensdatenbanken werden erstellt und mit Agenten verknüpft. Sobald verknüpft, versucht der Agent vor jeder Antwort automatisch, passende Informationen abzurufen – der Prompt muss dafür nicht angepasst werden. Beim Erstellen werden Quellen zerlegt („chunked"), eingebettet („embedded") und in einer Vektordatenbank gespeichert. Während des Anrufs nutzt der Agent das bisherige Transkript (ohne Prompt), um relevante Abschnitte zu finden und dem LLM als Kontext zuzuführen.

### Auto-refreshing & Auto-crawling

- **Automatisches Aktualisieren:** Ruft alle 24 Stunden alle URLs neu ab, damit die neuesten Inhalte berücksichtigt werden.
- **Automatisches Crawlen:** Crawlt alle 24 Stunden alle Seiten unter einem Pfad (außer Ausschlussliste). Gefundene Seiten werden gespeichert.

## Limits

| Quelle | Limit |
| --- | --- |
| URL | max. 500 URLs |
| Auto-Crawling | max. 200 Ausschluss-URLs je Pfad, max. 500 je Wissensdatenbank |
| Text | max. 50 Textausschnitte |
| Datei | max. 25 Dateien, je max. 50 MB; CSV/TSV/XLS/XLSX: max. 1000 Zeilen, 50 Spalten |

Mehrere Wissensdatenbanken erstellen, um Limits zu umgehen. Ein Agent kann mit mehreren Datenbanken verknüpft sein.

## Best Practices

- `.md` (Markdown) gegenüber `.txt` bevorzugen – gut strukturiertes Markdown wird genauer zerlegt und abgerufen.
  - Klare, beschreibende Überschriften; jeden `##`-Abschnitt fokussiert und kurz halten. Zu lange Bereiche in mehrere `##`/`###` unterteilen.
  - Kurze Absätze und Listen statt Textwände.
  - Bei tabellen- oder bildlastigen Inhalten ist der Abruf weniger zuverlässig – erläuternden Text ergänzen.
- Verwandte Informationen im selben Abschnitt gruppieren.
- Mehrdeutigkeiten vermeiden, spezifische Referenzen nutzen: Namen, Daten und Einheiten nennen; Pronomen wie „es" oder „dies" vermeiden (vorherige Abschnitte können im Abruf fehlen).
- Granulare Pfade fürs Auto-Crawling statt breiter Pfade mit vielen Ausschluss-URLs.
- Knowledge Base nur für unterstützende Informationen nutzen – Anweisungen/Prompts gehören in den Agenten-Prompt.

## Knowledge Base nutzen

1. **Einstellungen öffnen:** Dashboard → Reiter **Knowledge Base** → oben rechts **Add**.
2. **Elemente erstellen** aus drei Quellarten:
   - **URL:** Inhalt von Webseiten importieren (einzelne Seiten oder ganze Websites; automatische Aktualisierung).
   - **File:** Dokumente hochladen (PDF, TXT, DOCX usw.; max. 50 MB).
   - **Text:** Benutzerdefinierten Inhalt hinzufügen.
3. **Automatisches Crawlen aktivieren:** Für einzelne URL-Pfade. Nicht ausgewählte URLs landen auf der Ausschlussliste.
4. **Hinzugefügte Elemente prüfen:** Erscheinen in der Liste; anzeigen, bearbeiten oder löschen.
5. **Mit dem Agenten verbinden:** Agenten-Editor → Abschnitt **Knowledge Base** → Elemente auswählen.
6. **Einstellungen konfigurieren:**
   - **Chunks to retrieve:** Max. Anzahl abzurufender Abschnitte (1–10, Standard: 3).
   - **Similarity Threshold:** Wie strikt abgeglichen wird (Standard: 0.6). Höher = weniger, aber ähnlichere Treffer.
   - Hinweis: Mehr Chunks geben mehr Kontext, erhöhen aber die Prompt-Länge und können die Qualität beeinträchtigen.
7. **Auf Knotenebene (Conversation Flow Agent):** Wissensdatenbanken auf Ebene der Conversation Nodes und Subagent Nodes konfigurierbar; werden mit der Agentenebene kombiniert. Abgerufener Inhalt wird unter `## Related Knowledge Base Contexts` an den LLM-Prompt angehängt.

## Preise

- **Erstellung:** Die ersten 10 Wissensdatenbanken kostenlos, danach 8 \$ / Monat pro Wissensdatenbank.
- **Nutzung:** 0,005 \$ pro Minute bei Anrufen mit aktivierter Wissensdatenbank (unabhängig von der Anzahl verknüpfter Datenbanken).

## Trends4Markets-Default

| Einstellung | Wert |
| --- | --- |
| Chunks to retrieve | 6–7 Chunks |
| Similarity Threshold | 0.4–0.5 |