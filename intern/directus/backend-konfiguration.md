---
title: "Directus-/Backend-Konfiguration"
audience: ["admin", "prompt_engineer"]
product: "intern"
module: "directus"
route: "/directus/backend-konfiguration"
tags: ["directus", "backend", "partner", "kontakte"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Directus-/Backend-Konfiguration

## Was ist das?

Die Backend-seitige Konfiguration in Directus für einen Partner/Kunden: Partner-ID, Partner-Informationen und Kontakte. Die praktische Anlage eines Partners in Directus ist zusätzlich beschrieben unter [Vom neuen Projekt zum Voice Agent](/intern/onboarding/vom-projekt-zum-bot) (Abschnitte „Partner / Kunde in Directus anlegen" und „Agent in Directus einfügen").

## Partner-ID

Die **Partner-ID** ist die eindeutige Kennung eines Kunden/Partners in Directus. Sie entspricht der **Retell-ID** und wird in den Retell-Functions als `partnerID` verwendet — darüber werden Anrufe, Agents, Knowledge und User dem richtigen Partner zugeordnet.

Wichtig: Die `partnerID` in einer Retell-Function muss mit der Partner-ID im Directus-Backend übereinstimmen (siehe auch [Funktionen & Custom Functions](/intern/retell/funktionen)).

## Partner-Informationen

Die Stammdaten eines Partners im Partner-Datensatz. Die wichtigsten Felder:

- **Company Name** (Pflichtfeld): offizieller Firmenname des Kunden.
- **Display Name** (Pflichtfeld): Anzeigename, der in der TrendVoice-App bzw. im Widget verwendet wird.
- **Email Rueckruf CC**: CC-Adresse, die bei Rückruf-Mails in Kopie gesetzt wird.
- **Lead Notification Email**: Adresse, an die Benachrichtigungen über neue Leads gehen.
- **Feed URL**: optionales Feld, bei den meisten Partnern leer; derzeit ungenutzt, die Funktion ist nicht dokumentiert.
- **Logo** (Pflichtfeld): Unternehmenslogo (u. a. fürs Chat-Widget).
- **Business Image**: repräsentatives Bild des Unternehmens (z. B. Gebäude/Eingang).

Weiter unten im Partner-Datensatz folgen zahlreiche weitere Felder (Auswahl):

**Darstellung**

- **Markenfarbe (Color):** Unternehmensfarbe (meist aus dem Logo), u. a. in Oberfläche und Chat-Widget.
- **Status:** Veröffentlichungsstatus des Partners (z. B. veröffentlicht).

**Retell-Anbindung**

- **Retell Org ID:** Workspace-/Organisations-ID aus Retell (Settings → Workspace).
- **API Key:** Retell-API-Key des Workspaces. Wichtig: Hier muss der **Secret Key** aus Retell eingetragen werden (nicht der Public Key) — nur damit funktionieren die Webhooks korrekt.
- **Agent ID:** Inbound-(Haupt-)Agent.
- **Outbound Agent ID:** Agent für ausgehende Anrufe.
- **Override Agent ID:** Override-Agent.
- **Chat Agent ID:** Chat-Agent.
- **Chat Public Key:** öffentlicher Schlüssel für die Einbindung des Chat-Widgets.

**Telefonie (Twilio)**

- **In- & Outbound Number:** Telefonnummern für eingehende und ausgehende Anrufe.
- **Twilio Account SID:** Kennung des Twilio-(Sub-)Accounts.
- **Twilio Auth Token:** Auth-Token des Twilio-Accounts.

**Weitere**

- **Users:** mit dem Partner verknüpfte Benutzer (Anlage/Verknüpfung siehe [Onboarding](/intern/onboarding/vom-projekt-zum-bot)).
- **Business Hours:** Geschäftszeiten des Partners (steuern u. a. die Erreichbarkeit der Agenten).
- **Adressdaten:** weitere Adressfelder des Unternehmens.
- **API-Verbindungen (Integrationen):** Anbindungen an externe Systeme wie Zendesk oder Microsoft Teams.

Die praktische Befüllung der Retell-/Telefonie-Felder ist zusätzlich im [Onboarding-Kapitel](/intern/onboarding/vom-projekt-zum-bot) beschrieben (Abschnitt „Retell-Daten in Directus einfügen").

!!! warning "Sensible Felder" Felder wie **API Key**, **Twilio Auth Token** und **Chat Public Key** enthalten Zugangsdaten/Geheimnisse — in Screenshots maskieren und nicht weitergeben.

## Kontakte

Directus hält für Kontakte/Nutzer drei getrennte Collections. Zur Einordnung, damit nichts verwechselt wird:

- **User Directory (Alle Benutzer):** hier werden die **Accounts der TrendVoice-App-Nutzer** verwaltet — erstellen, bearbeiten, löschen. Enthält Name, Partnerzugehörigkeit, Zugangsdaten sowie die Rolle mit den zugehörigen Berechtigungen (z. B. `TrendVoice-Owner`, `TrendVoice-User`, `Administrator`). Die praktische Anlage ist im [Onboarding-Kapitel](/intern/onboarding/vom-projekt-zum-bot) beschrieben (Abschnitte „Benutzer in Directus anlegen" und „User-Menü in Directus").
- **Partners:** enthält alle TrendView-Kunden (als Unternehmen), die die TrendVoice-App nutzen — siehe [Partner-Informationen](#partner-informationen) oben.
- **Lead Contacts:** hier werden **alle Kontakte aus Leads** gespeichert (unabhängig vom Lead-Typ). Das Backend nutzt diese Collection, um die über Lead-Formulare erfassten Kontakte abzuspeichern und bei Bedarf Nachrichten/Benachrichtigungen an den passenden Kontakt zu senden.

Kurz: **User Directory** = wer darf sich in der TrendVoice-App anmelden, **Partners** = welches Kunden-Unternehmen, **Lead Contacts** = welche Person hat über ein Lead-Formular Kontakt aufgenommen.
