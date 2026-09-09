---
title: "Analytics"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "monitoring"
route: "/monitoring/analytics"
tags: ["retell", "monitoring", "analytics"]
visibility: "internal"
version: "2026-08"
doc_status: "published"
---

# Analytics

## Was ist das?

Im Analytics-Bereich baut ihr eigene Auswertungs-Widgets über Call-Metriken (z. B. Anzahl Anrufe, Kosten) — als einzelne Kennzahl oder als Zeitverlauf, mit Filtern und optionaler Aufschlüsselung.

## Wofür brauchen wir das?

Für den schnellen visuellen Überblick über Anrufvolumen und Kosten pro Projekt/Agent — ergänzend zu den automatisierten [Alerts](/intern/retell/monitoring/alerts), die nur bei Schwellenwert-Überschreitung reagieren.

## Aufbau eines Analytics-Widgets

| Abschnitt | Inhalt |
| --- | --- |
| **Graph Type** | Darstellung des Widgets, z. B. `Number` (einzelne Kennzahl) oder `Column` (Säulendiagramm über die Zeit). |
| **Call Source Metrics** | Metrik (z. B. _Call Counts_, _Combined Cost_) sowie bei manchen Metriken eine Aggregation (z. B. _Sum_). |
| **Filter** | Grenzt die Datenbasis ein, z. B. auf bestimmte Agenten. |
| **Breakdown** | Nur bei Zeitverlauf-Diagrammen: zusätzliche Aufschlüsselung der Werte, z. B. je Agent als eigene Datenreihe. |
| **Vorschau** | Live-Vorschau des Widgets mit einstellbarem `Date Range` (z. B. _Last 1 week_, _Last 3 months_) und Ansicht (Hour/Day/Week/Month). |

## Beispiele (Trends4Markets)

### Combined Cost als Zahl

{/* ![Analytics Combined Cost als Zahl](/images/retell/retell-analytics-number-combined-cost.png) – Bild fehlt, bitte hochladen */}

| Feld | Wert |
| --- | --- |
| Graph Type | Number |
| Metrik | Combined cost |
| Aggregation | Sum |
| Filter | Agent (2 agents) |
| Date Range | Last 1 week |
| Ergebnis | \$22.821 |

### Call Counts als Zahl

![Analytics Call Counts als Zahl](/images/retell/retell-analytics-number-call-counts-2.png)

| Feld | Wert |
| --- | --- |
| Graph Type | Number |
| Metrik | Call Counts |
| Filter | Agent (2 agents) |
| Date Range | Last 3 months |
| Ergebnis | 2.706 |

### Combined Cost als Säulendiagramm

![Analytics Combined Cost als Säulendiagramm](/images/retell/retell-analytics-column-combined-cost-2.png)

| Feld | Wert |
| --- | --- |
| Graph Type | Column |
| Metrik | Combined cost |
| Aggregation | Sum |
| Filter | Agent (2 agents) |
| Breakdown | Agent |
| Date Range | Last 1 week, Ansicht Day |
| Y-Achse | $$0.00 – $$8.00 |
| X-Achse | Aug 04 – Aug 11 |

### Call Counts als Säulendiagramm

![Analytics Call Counts als Säulendiagramm](/images/retell/retell-analytics-column-call-counts-2.png)

| Feld | Wert |
| --- | --- |
| Graph Type | Column |
| Metrik | Call Counts |
| Filter | Agent (2 agents) |
| Breakdown | Agent |
| Date Range | Last 3 months, Ansicht Month |
| Y-Achse | 0 – 1.0K |
| X-Achse | May 01 – Aug 01 |