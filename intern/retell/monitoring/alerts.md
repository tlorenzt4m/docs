---
title: "Alerts"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "monitoring"
route: "/monitoring/alerts"
tags: ["retell", "monitoring", "alerts"]
visibility: "internal"
version: "2026-08"
doc_status: "published"
---

# Alerts

## Was ist das?

Alerts überwachen Call-Metriken (z. B. Anzahl Anrufe, Kosten) automatisiert in festen Zeitabständen und benachrichtigen euch, sobald ein definierter Schwellenwert überschritten wird.

## Wofür brauchen wir das?

Damit ungewöhnliches Anrufvolumen oder unerwartet hohe Kosten pro Projekt sofort auffallen — ohne dass jemand manuell im Dashboard nachschauen muss.

## Aufbau eines Alerts

| Abschnitt | Inhalt |
| --- | --- |
| **Alert Name** | Freitext-Bezeichnung, beschreibt Bedingung und Schwellenwert. |
| **Time Configuration** | `Check every` (Prüfintervall) \+ `for the last` (Betrachtungszeitraum der Metrik). |
| **Metric Condition** | `Modus` — _Compare to certain value_ (fester Schwellenwert) oder _Compare to last cycle_ (Vergleich zum vorherigen Zeitfenster); `Metrik` (z. B. _Number of Calls_, _Total Call Cost_); `Bedingung` (Operator wie _is above_ / _is equal or above_ \+ Wert). |
| **Filter** | Grenzt den Alert auf bestimmte Agenten ein (z. B. Override- und Live-Variante desselben Agenten gemeinsam). |
| **Notify via** | E-Mail-Adressen und/oder Webhook-URL, die bei Auslösen benachrichtigt werden. |

!!! warning "Webhook-Payload bei Kostenmetriken: Cent statt Dollar" Bei den Metriken `total_call_cost` und `total_chat_cost` sind `current_value`, `previous_value` und `threshold_value` im Webhook-Payload in **Cent** angegeben — das Dashboard zeigt dieselben Werte dagegen in **Dollar** an. Beim Verarbeiten des Webhooks (z. B. im Backend) muss durch 100 geteilt werden, um auf den im Dashboard sichtbaren Dollarbetrag zu kommen.

## Beispiele (Trends4Markets)

### Tageslimit Anrufe

![Edit Alert – Tageslimit Anrufe](/images/retell/retell-alert-edit-tageslimit-anrufe-2.png)

| Feld | Wert |
| --- | --- |
| Alert Name | Überschreitung des Tageslimits an Anrufen \>= 50 Inbound / Override \[Test\] |
| Check every | 1 hour |
| for the last | 24 hours |
| Modus | Compare to certain value |
| Metrik | Number of Calls |
| Bedingung | when sum is equal or above 50 |
| Filter | Agent: Inbound (Override), Inbound |
| Notify via | [ps@t4m.ai](mailto:ps@t4m.ai), [tl@t4m.ai](mailto:tl@t4m.ai); Webhook URL: (nicht gesetzt) |

### Kostenlimit pro Woche

![Edit Alert – Kostenlimit pro Woche](/images/retell/retell-alert-edit-kostenlimit-woche-2.png)

| Feld | Wert |
| --- | --- |
| Alert Name | Überschreiten eines Limits von 30,- EUR Kosten pro Woche \[Test\] |
| Check every | 24 hours |
| for the last | 7 days |
| Modus | Compare to certain value |
| Metrik | Total Call Cost |
| Bedingung | when sum is equal or above \$ 30 |
| Filter | Agent: Inbound (Override), Inbound |
| Notify via | [ps@t4m.ai](mailto:ps@t4m.ai), [tl@t4m.ai](mailto:tl@t4m.ai); Webhook URL: (nicht gesetzt) |

!!! note "Werte projektabhängig, Beispiele als \[Test\] markiert" Schwellenwerte, Filter und Empfänger sind pro Kunde/Projekt individuell zu setzen — die obigen Werte stammen aus einem konkreten Testaufbau (Namen tragen den Zusatz „\[Test\]"), keine festen Trends4Markets-Defaults.

## Häufige Probleme

| Problem | Lösung |
| --- | --- |
| Alert löst nicht aus | `Check every`/`for the last` und Bedingung (Schwellenwert, Vergleichsoperator) prüfen — Zeitfenster muss zur erwarteten Metrik passen. |
| Keine Benachrichtigung erhalten | E-Mail-Adressen unter „Notify via" und ggf. Spam-Ordner prüfen; Webhook-URL auf Erreichbarkeit testen. |