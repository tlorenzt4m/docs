---
title: "Vom Projekt Zum Bot"
---

# Vom neuen Projekt zum Voice Agent

## Was ist das?

Der vollständige Konfigurationsablauf vom Start eines neuen Kundenprojekts bis zu einem fürs Testen fertig konfigurierten Voice-Agenten bzw. Bot. Die Schritte sind chronologisch geordnet und durchlaufen alle beteiligten Systeme: Awork, Retell, Twilio und Directus.

## Wofür brauchen wir das?

Damit das Onboarding eines neuen Kunden reproduzierbar und ohne Lücken abläuft – von der Workspace-Anlage über die Telefonie bis zur Übergabe der Zugangsdaten.

!!! info "Phasenüberblick"<br />    1. Vorbereitung und Retell-Grundeinrichtung<br />    2. Twilio einrichten<br />    3. SIP Trunk im Kunden-Workspace<br />    4. Retell mit Twilio verbinden<br />    5. Partner / Kunde in Directus anlegen<br />    6. User-Menü in Directus<br />    7. Agent in Directus einfügen<br />    8. TrendVoice App prüfen<br />    9. Benutzer in Directus anlegen<br />    10. Zugangsdaten an Kunden schicken

## 1. Vorbereitung und Retell-Grundeinrichtung

### Vorbereitung in Awork

- Awork-Projekt anschauen.
- Aufgaben anschauen.

### Start in Retell

1. In Retell einloggen.
2. **Add another workspace** auswählen.
3. Benennung: nach Kundenname.
4. Kreditkarte muss hinterlegt werden.
5. Unter **Settings → Workspace → Users**: `d.mittellmann` als Admin hinzufügen.
6. Workspace mit `info@trendview.de` hinzufügen.
7. Demo-Agenten löschen.

!!! warning "Voraussetzung fürs Testen"<br />    Testen geht erst, wenn Dennis die Kreditkarte hinzugefügt hat.

### Agent in Retell anlegen oder importieren

Wenn keine Agents mehr vorhanden sind, entweder einen neuen Agent anlegen oder einen bestehenden übernehmen:

1. Einen schon etwas gefüllten Agent exportieren – über die drei Punkte oben rechts im Menü.
2. Zurück in den neuen Workspace wechseln.
3. Import im gewünschten Workspace durchführen – mit der zuvor exportierten JSON-Datei.

!!! note "Mögliche Fehler beim Import"<br />    Manche Sachen können nicht importiert werden, zum Beispiel **Stimme**, **Telefonnummer** und **Knowledge Base**.

!!! tip "Fehlerlösung bei Stimme"<br />    Eine Default-Stimme auswählen (unter **Alle Typen** zu finden) und danach erneut versuchen, den Agent einzufügen.

### Agenten duplizieren und benennen

Im Workspace den Agent nochmal duplizieren. Danach sollten zwei Agents vorhanden sein:

- **Inbound Agent** (Hauptagent)
- **Override Agent**

### Knowledge Base hinzufügen

- Zuerst die Webseite des Kunden hinzufügen.
- Links gehen immer nur bis 500. Deshalb in der Link-Liste immer 500 auswählen und häppchenweise als Knowledge hinzufügen.

Beispiel:

| Block | Links |
| :-- | :-- |
| Webseite 1 | erste Links bis 500 |
| Webseite 2 | ab dem 500. Link bis 1000 |
| … | usw. |

## 2. Twilio einrichten

### Telefonnummer in Twilio holen

- Auf `twilio.com/login` einloggen.
- Mit folgender E-Mail-Adresse einloggen: `info@trendview.de`

### Subaccount erstellen

1. Links oben auf **Trendview GmbH** klicken.
2. **View Subaccs** auswählen.
3. Rechts auf **Create new Subacc** klicken.
4. Den gleichen Namen verwenden wie in Retell: **Workspace-Name = Subaccount-Name**.
5. Danach im Subaccount weitermachen.

### Falls Optionen nicht angezeigt werden

Falls **SIP Trunk** und **Phone Numbers** nicht angezeigt werden:

- Links im Menü auf **Explore Products** gehen.
- Dort die Produkte raussuchen.
- Auf den Pin klicken.
- Irland auswählen.

### Bundle erstellen

- Erstmal ein Bundle erstellen.
- Das ist einmalig für den neuen Kunden.
- Siehe dazu Schritt 3 im Wizard.

### Nummer kaufen

1. In Twilio zu **Phone Numbers** gehen.
2. **Ireland → Manage → Buy a number** auswählen.
3. Country: Germany.
4. Vorwahl vom Kunden nehmen – ohne Null suchen.
5. In der **Advanced Search** suchen, Kriterium: Number.
6. Nummer auswählen.

!!! warning "Eingetragene Firma erforderlich"<br />    Eine Nummer bekommt man nur, wenn man eine eingetragene Firma ist.

### Wizard / Regulatory Requirements

- Durch den Wizard klicken.
- Comply Regulatory Requirements in Retell kann man mit einem Eintrag aus dem Handelsregister erfüllen.

!!! note "Bei Fehlern"<br />    Rechts auf **Jump to Regulatorys** klicken und zu **Bundles** gehen.

**Angaben im Bundle:**

| Feld | Wert |
| :-- | :-- |
| Identity Type | Direct Customer |
| Who will answer… | Business |

**Business Information:**

- `Trendview.de` verwenden.
- Steuernummer siehe Webseite.
- In **Business Website** die Trendview-Webseite einfügen.
- Alternativ: Kundenwebseite, Kundeninfos.

**Adresse:**

- Ferdinand-Nebel-Straße / Ferdinand Nebel.
- Kundenadresse verwenden.

**Authorized Representative:**

- Name siehe Awork.
- Weitere Daten einfügen.

**Supporting Docs Requirements:**

- Proof: Handelsregisterauszug – [https://www.handelsregister.de/rp\_web/welcome.xhtml](https://www.handelsregister.de/rp_web/welcome.xhtml)
- In den anderen beiden Dropdowns Handelsregister auswählen.

**Finaler Schritt im Bundle:**

- Bundle einen Namen geben.
- Notification-E-Mail angeben.
- Immer die eigene Mail von einem aus dem AI-Team angeben (derjenige, der die Erstellung macht).
- Hier einmal die Kundensachen einfügen, falls vorhanden.
- Bei Fehlern die Daten mit Trendview-Daten füllen.

## 3. SIP Trunk im Kunden-Workspace

### SIP Trunk erstellen

Im Kunden-Workspace weitermachen.

- Links mittig unter **Errors & Warnings**.
- **Create new SIP Trunk** auswählen.
- Kundenname eingeben.

### SIP Trunk: General

1. Menüpunkt **General** öffnen.
2. Runterscrollen.
3. **Call Transfer** enablen.
4. **Enable PSTN Transfer** aktivieren.
5. Auf **Save** klicken.
6. Einmal hochscrollen und prüfen, ob es gespeichert wurde.

### SIP Trunk: Termination

1. Menüpunkt **Termination** öffnen.
2. Bei **Termination SIP URI** kundenspezifisches eintragen: Kundenname ohne Bindestrich.
3. Aus dem Feld klicken.
4. Verfügbarkeit checken lassen.
5. **Show localized URIs** anzeigen lassen.
6. **Europe Frankfurt** auswählen.

**Authentication:**

- Bei **Credential Lists** den Kundennamen eintragen.
- Username für den Kunden erstellen.
- Passwort generieren lassen.
- IP Access Control List brauchen wir nicht.
- Ganz unten wieder auf **Save** klicken und Update checken.

### SIP Trunk: Origination

- Menüpunkt **Origination** öffnen.
- Bei **Add new Origination URI** immer Folgendes im obersten Feld einfügen:

```text
sip:sip.retellai.com
```

### SIP Trunk: Numbers

1. Menüpunkt **Numbers** öffnen.
2. Rechts auf **Add a Number** klicken.
3. **Existing Number** auswählen: nicht konfigurierte Nummer auswählen.

## 4. Retell mit Twilio verbinden

### Zu Retell wechseln

- In den Kunden-Workspace wechseln.
- Zu **Deploy → Phone Numbers** gehen.
- Auf das Plus klicken.
- **Connect to your number via SIP trunking** auswählen.
- Die gekaufte Nummer einsetzen.

**Angaben einfügen:**

- Termination URI: URI einfügen, die zuvor erstellt wurde.
- SIP Trunk Username: Kundenname nutzen.
- Alles aus Twilio übernehmen.
- Passwort: wie in Twilio.
- Nickname: Kundenname / Agent Name.

### Agent und Webhook verbinden

- Dem SIP Trunk den Inbound Call Agent hinzufügen.
- Webhook hinzufügen: Standard-Webhook einfügen (aus Directus oder aus einem anderen Agent kopieren).

### Testanruf

Einmal einen Testanruf machen.

## 5. Partner / Kunde in Directus anlegen

### Partner erstellen

- In Directus ins Menü **Partners** gehen.
- Rechts auf **Element erstellen** klicken.
- Kundenname einfügen.

**Felder ausfüllen:**

- Display Name: gleich Kundenname.
- Business Image: vom Kunden einfügen (z. B. Unternehmenseingang o. Ä.).
- Kundenlogo suchen und einfügen.
- Color Picker: Farbe aus dem Logo nehmen.
- Status: veröffentlicht.

### Retell-Daten in Directus einfügen

| Daten | Quelle in Retell |
| :-- | :-- |
| Retell Org ID | Settings → Workspace → Workspace ID kopieren |
| Retell API Key | API Keys → Key kopieren |
| Agent ID | Agents → Hauptagent → im Promptfenster rechts die Agent ID kopieren |
| Override Agent | wie oben einfügen |
| Inbound Number | Inbound Number aus Retell kopieren |

Jeweils in Directus einfügen.

### User zum Partner hinzufügen

Folgende User immer hinzufügen: **Phillip, Stefan, Dennis, Matthias, Tim, Kunde**.

Danach oben rechts auf den Haken klicken, um zu speichern.

## 6. User-Menü in Directus

### User mit Partner verknüpfen

- Im User-Menü wie oben Stefan, Phillip, Dennis, Matthias, Tim etc. einfügen.
- Unter dem Menüpunkt **Partners** den neuen Kunden im Bulk Edit suchen.
- Partner eintragen.
- Mit dem Haken bestätigen.

!!! warning "Immer beidseitig verknüpfen"<br />    - Im Partner die User hinzufügen.<br />    - Beim User den Partner hinzufügen.

## 7. Agent in Directus einfügen

### Collection / Menü Agents

- In Directus zur Collection / zum Menü **Agents** gehen.
- Retell Inbound und Override hinzufügen.
- Auf das Plus klicken.

**Inbound Agent eintragen:**

| Feld | Wert |
| :-- | :-- |
| ID | Agent ID hinzufügen |
| Name | Inbound Name einfügen |
| Type | inbound |
| Status | veröffentlicht |
| Retell LLM ID | aus Retell kopieren |
| Begin Message | aus Retell einfügen |
| Prompt General | gesamten Prompt aus Retell einfügen |

**Partner zuordnen:** Unter **Partner** den Kunden-Agent einfügen.

**Override Agent:** Für den Override Agent die Schritte wiederholen.

## 8. TrendVoice App prüfen

### Funktionstest in der TrendVoice App

- In der TrendVoice App prüfen, ob alles funktioniert.
- Unter **Partner** checken, ob der Partner zu sehen ist.

### Demo-Zwecke

- Einmal Kontakt einfügen.
- Zweckweise Anrufe tätigen.
- Verschiedene Funktionen triggern.

## 9. Benutzer in Directus anlegen

### Alle Benutzer anlegen

- In Directus zu **Alle Benutzer** gehen.
- Rechts auf das Plus klicken.
- Daten aus Awork etc. oder aus dem Termin übernehmen.
- Alle vorhandenen Daten einfügen.
- Passwort erstellen lassen.

### Admin-Optionen setzen

Ganz weit nach unten scrollen bis zu den roten Admin-Optionen.

- **Rolle:** TrendVoice-Owner
- **Policies:** Unter **Policies → Vorhanden** ganz runter scrollen und folgende Rollen / Policies hinzufügen: TrendVoice, Switchboard, Knowledge, SMS.

### Partner hinzufügen

- Runterscrollen bis **Partners**.
- Partner hinzufügen: Kundenname.

### Feature Flags setzen

**Default Features:**

- Feature TrendVoice
- Feature Switchboard
- Feature Show Recording Files

**Für Integrationen zusätzlich:**

- Feature Show Call Details
- Feature TrendVoice Integrations

!!! note "Sonderfall Fahrrad Franz"<br />    Fahrrad Franz bekommt zusätzlich **Feature Zendesk**.

## 10. Zugangsdaten an Kunden schicken

### Passwort über OneTimeSecret teilen

- `onetimesecret.com` öffnen.
- Passwort einfügen.
- Link erzeugen.

### User und Partner gegenseitig verknüpfen

- Im User-Menü den Partner hinzufügen.
- Im Partner-Menü den User hinzufügen.

### Zugangsdaten per E-Mail senden

Die Zugangsdaten dann per E-Mail senden. Dabei verwenden:

- den `onetimesecret.com`-Link für das Passwort
- die E-Mail-Adresse

## Ergebnis prüfen

- Testanruf auf der neuen Twilio-Nummer wird vom Inbound Agent angenommen.
- Partner, User und Agents sind in Directus angelegt und beidseitig verknüpft.
- Partner und Funktionen sind in der TrendVoice App sichtbar.
- Feature Flags sind gesetzt.
- Zugangsdaten wurden über OneTimeSecret-Link an den Kunden versendet.

## Häufige Probleme

| Problem | Lösung |
| :-- | :-- |
| Testanruf nicht möglich | Kreditkarte in Retell hinterlegt? (durch Dennis) |
| Stimme/Telefonnummer/KB nach Import fehlt | Diese werden nicht importiert – Default-Stimme unter **Alle Typen** wählen und manuell ergänzen |
| Keine Twilio-Nummer kaufbar | Setzt eine eingetragene Firma voraus; Regulatory Requirements / Bundle prüfen |
| Partner taucht in der App nicht auf | User und Partner in Directus beidseitig verknüpfen |
| Optionen (SIP Trunk / Phone Numbers) fehlen in Twilio | Über **Explore Products** anpinnen, Irland auswählen |