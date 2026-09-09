---
title: "Weitere Retell-Einstellungen"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/weitere-einstellungen"
tags: ["retell", "speech", "transcription", "call-settings", "webhook", "mcp", "security"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Weitere Retell-Einstellungen

Sammelseite für die übrigen Retell-Einstellungsbereiche mit den jeweiligen Trends4Markets-Defaults.

## Speech Settings

Optionen zur Feinabstimmung der Interaktion:

- **Background sound:** Durchgehendes Hintergrundgeräusch (z. B. Callcenter-Atmosphäre), um das Gespräch menschlicher zu gestalten.
- **Responsiveness:** Wie schnell der Agent antwortet. Niedrigere Werte = längere Wartezeiten (z. B. bei älteren Menschen). „Dynamisch anpassen" passt das Timing automatisch ans Sprechtempo an.
- **Interruption Sensitivity:** Wie schnell der Agent auf Unterbrechungen reagiert. Niedrigere Werte machen ihn widerstandsfähiger gegen Hintergrundgeräusche.
- **Backchanneling:** Wie oft und mit welchen Worten (z. B. „Mhm", „Verstehe") der Agent Zuhören signalisiert.
- **Boosted Keywords:** Bevorzugt bestimmte Wörter (z. B. Marken-, Personennamen) für höhere Erkennungsrate.
- **Speech Normalization:** Wandelt Einheiten wie Daten, Währungen oder Zahlen in ausgeschriebene Wörter um.
- **Reminder frequency:** Wie oft der Agent den Nutzer bei Inaktivität anspricht.
- **Pronunciation:** Ausspracheleitfaden für spezifische Wörter.

**Trends4Markets-Default:**

| Einstellung | Wert |
| --- | --- |
| Background Sounds | Keine |
| Responds Eagerness | 1 |
| Dynamical Adjust | Aus |
| Interrupt Sensitivity | 0.8–0.85 |
| Reminder Message Frequency | 8–12 sec, 1 time |
| Pronunciation | Lautschrift für ungewöhnlich ausgesprochene Wörter/Satzteile |

## Realtime Transcription Settings

Die Realtime-Transcription-Settings steuern, wie die gesprochene Sprache während des Anrufs in Text umgewandelt wird. Die Transkriptionsqualität hängt vor allem von den eingesetzten ASR-Modellen ab, die zwischen Genauigkeit und Geschwindigkeit abwägen. Über die folgenden Einstellungen lässt sie sich gezielt verbessern:

- **Denoising mode (Rauschunterdrückung):** Filtert Hintergrundgeräusche heraus. Bei viel Lärm hilft stärkeres Denoising. In ruhiger Umgebung kann es jedoch kurze, leise Antworten wie „ja" oder „klar" herausfiltern — dann besser auf _No Denoising_ stellen, damit das Roh-Audiosignal erhalten bleibt und solche kurzen Äußerungen erkannt werden.
- **Transcription mode:** Optimiert die Transkription. Wenn Sätze zu früh „abgeschnitten" werden (der Text wird als final ausgegeben, bevor der Satz zu Ende ist), den auf **Genauigkeit** optimierten Modus aktivieren.
- **Boosted Keywords:** Eigene Schlüsselwörter, die das Vokabular des Modells erweitern — gedacht für Spezial- und Fachbegriffe oder schwer erkennbare Wörter (z. B. Firmen-/Produktnamen, „Retell"). Bis zu **100** Keywords möglich. Sparsam einsetzen: zu viele Keywords verschlechtern die Erkennung eher.
- **Endpointing:** Wartezeit (in Sekunden), nach der eine Sprechpause als Ende der Äußerung gewertet wird. Niedrigere Werte lassen den Agenten schneller reagieren, können aber längere Sätze vorzeitig abschneiden.
- **Custom settings (ASR-Provider):** Auswahl des Transkriptionsanbieters/-modells (bei uns: Soniox).

Übersetzt/zusammengefasst aus der Retell-Doku „Increase transcription accuracy" (`https://docs.retellai.com/build/increase-transcription-accuracy`).

**Trends4Markets-Default:**

| Einstellung | Wert |
| --- | --- |
| Denoising mode | remove noise |
| Transcription mode | (projektabhängig) |
| Custom settings | provider: soniox |
| Endpointing | 1.38 |
| Boosted Keywords | schwierige Firmennamen o. Ä.; nicht zu viele Keywords hinterlegen |

## Call Settings

Die Call-Settings betreffen den betrieblichen Ablauf eines Anrufs — also wie er beginnt, endet und mit Sonderfällen umgeht:

- **Voicemail detection:** Erkennt, ob statt einer Person ein Anrufbeantworter abnimmt, und legt fest, was dann passiert (z. B. auflegen oder eine Nachricht hinterlassen). Vor allem bei ausgehenden Anrufen relevant.
- **End call on silence:** Beendet den Anruf, wenn der Nutzer eine bestimmte Zeit lang inaktiv ist.
- **Max Call duration:** Maximale Gesamtdauer eines Anrufs; danach wird automatisch beendet.
- **Pause before speaking:** Spricht der Agent zuerst (Agent-First), wartet er zu Beginn die eingestellte Zeit, bevor er loslegt — nützlich, während der Nutzer den Hörer noch abnimmt. (Diese Zeit setzen wir in der Regel bei der [Welcome Message](/intern/retell/welcome-message).)

Die weiteren Schalter im Trends4Markets-Default sind in der verlinkten Retell-Übersicht nicht näher beschrieben; ihre genaue Wirkung im Zweifel direkt in Retell prüfen:

- **Ring duration:** Wie lange es klingelt, bevor der (ausgehende) Anruf abgebrochen wird.
- **IVR hangup:** Verhalten, wenn statt einer Person ein automatisches Sprachmenü (IVR) erkannt wird.
- **User keypad:** Ob Tastatureingaben des Nutzers (DTMF-Töne) während des Anrufs verarbeitet werden.
- **iOS:** iOS-spezifische Anrufbehandlung — genaue Wirkung in Retell verifizieren.

Zusammengefasst aus der Retell-Doku „Step 2: Configure the basic settings" → _Configure Call Settings_ (`https://docs.retellai.com`).

**Trends4Markets-Default:**

| Einstellung | Wert |
| --- | --- |
| Voicemail detection | aus |
| iOS | aus |
| IVR hangup | aus |
| User keypad | aus |
| End call on silence | 20 s |
| Max Call duration | 8.0 m |
| Ring duration | 20 s |

## Post-Call Data Extraction

Nach jedem Anruf wertet Retell das Gespräch automatisch aus und extrahiert strukturierte Daten daraus (früher „Post-Call Analysis"). Die Auswertung läuft über konfigurierbare Prompts und ein eigenes Analyse-LLM.

**Eingebaute Analyse-Kategorien:**

- **Call Summary (`call_summary`):** Zusammenfassung des Gesprächs. Über den Prompt steuert ihr, welche Art von Zusammenfassung bzw. welche Details extrahiert werden.
- **Call Successful:** Bewertet per anpassbarem Prompt, ob der Anruf (oder Chat) erfolgreich war — ihr definiert eigene Erfolgskriterien.

Darüber hinaus lassen sich eigene Extraktionsfelder/-funktionen definieren, um gezielt Daten aus dem Gespräch zu ziehen.

**Beispiel: Einwilligung zur Gesprächsaufzeichnung (`custom_deny_consent`)**

| Feld | Wert |
| --- | --- |
| Name | `custom_deny_consent` |
| Typ | Boolean |
| Beschreibung | „Wenn der Anrufer der Gesprächsaufzeichnung widerspricht oder die Datenschutzbestimmungen nicht akzeptiert, dann trage hier true ein." |

Der Wert wird erst **nach** dem Anruf per Post-Call-Analyse gesetzt — der Widerruf greift technisch also im Nachgang (z. B. Löschung/PII-Scrubbing der Aufnahme, siehe [Security Fallback Settings](#security-fallback-settings)). Im Gespräch selbst bestätigt der Agent das „Stoppen" der Aufzeichnung nur mündlich (Prompt-Baustein „Widerspruch gegen die Gesprächsaufzeichnung" im [Prompt-Standard](/intern/retell/prompt-standard#praxisbeispiele-fur-sonderregeln)).

**Auswertung nachträglich neu berechnen (Rerun / Backfill):** Nach dem Anpassen der Prompts könnt ihr die Analyse für vergangene Anrufe neu laufen lassen — einzeln oder als Batch über **Call History → Actions → Backfill from Post-Call Data** (mit Filtern).

- Reruns nutzen immer die Analyse-Prompts der **aktuellen Draft-Version** des Agenten (nicht die zum Anrufzeitpunkt veröffentlichte) — Prompts also im Draft bearbeiten.
- ⚠️ Reruns/Backfills verursachen Kosten (für alle Modelle, auch solche, die beim ersten Lauf kostenlos waren); die Kosten skalieren mit der Anzahl der Sessions.
- Bei aktivierter CRM-Integration fließen die neu extrahierten Daten auch in die konfigurierten Mappings/Kontaktfelder.

Zusammengefasst aus der Retell-Doku „Rerun Post-Call/Chat Analysis" (`https://docs.retellai.com`).

**Trends4Markets-Default:**

- Wir übernehmen die Post-Call-Data-Extraction-Functions in der Regel aus einem bestehenden (anderen) Voice Agent, statt sie neu anzulegen.
- Analyse-LLM: **Gemini 3.0 Flash**

## Security Fallback Settings

Die Security-&-Fallback-Settings bündeln Datenschutz- und Ausfallsicherungs-Optionen des Agenten. Der zentrale Teil sind die **Data Storage Settings**.

**Data Storage Settings (Datenspeicherung):** Standardmäßig speichert Retell potenziell sensible Anrufdaten — u. a. Call-Logs, Transkripte, Aufnahmen, Caller-/Callee-ID, Knowledge-Base-Trefferlogs, Dynamic Variables und Metadaten. Drei Stufen sind wählbar:

- **Everything:** alles speichern (Transkripte, Aufnahmen, Logs).
- **Everything except PII:** Inhalte speichern, aber personenbezogene Daten (PII) nach dem Anruf entfernen (siehe unten).
- **Basic Attributes Only:** nur Metadaten — keine Transkripte/Aufnahmen/Logs. Diese Felder sind dann auch später nicht mehr über die Get-Call-API abrufbar.

Zusätzlich lässt sich eine **Data Retention Period** setzen, die gespeicherte Daten nach X Tagen automatisch löscht.

⚠️ **Wichtig beim Opt-out:** Auch ohne Speicherung erhaltet ihr weiterhin die Webhook-Events mit Transkript, Aufnahme etc. — der Link zur Aufnahme **läuft jedoch 10 Minuten** nach dem Webhook ab. Wer die Daten dauerhaft braucht, muss sie also zum Anrufzeitpunkt aus dem Webhook sichern.

**PII-Scrubbing (nur bei „Everything except PII"):** Konfigurierbare PII-Kategorien (z. B. `person_name`, `email`, `address`, `credit_card`, `bank_account`, `password`, `pin`, `date_of_birth`) werden nach dem Anruf erkannt und durch Platzhalter wie `[email 1]` ersetzt — in Transkript, Aufnahme (Piepton), Logs, Dynamic Variables, Metadaten, Call-Analyse und Tool-Calls. Die Rohoriginale werden gelöscht, nur die bereinigten Versionen bleiben.

- `phone_number` wirkt **gerichtet**: entfernt die **Kundennummer** (inbound: `from_number`, outbound: `to_number`) komplett — die eigene Retell-Nummer bleibt erhalten.
- Immer erhalten bleiben Kennungen/Timing/Outcome-Felder (z. B. `call_id`, `duration_ms`, `call_successful`); um auch diese loszuwerden → **Basic Attributes Only** oder Data Retention Period.

**Weitere Felder dieses Bereichs** (in der verlinkten Data-Storage-Doku nicht beschrieben):

- **Fallback voice id:** Ersatzstimme, falls der primäre Stimm-/TTS-Anbieter ausfällt (`automatic fallback` = automatische Wahl).
- **Default dynamic variables:** Standardwerte für Dynamic Variables, falls beim Anruf keine übergeben werden.
- **Opt-in secure URLs:** abgesicherte/signierte URLs für den Ressourcen-Zugriff — genaue Wirkung im Zweifel in Retell prüfen.

Zusammengefasst aus der Retell-Doku „Data Storage Settings" (`https://docs.retellai.com`).

**Trends4Markets-Default:**

| Einstellung | Wert |
| --- | --- |
| Data storage settings | basic attributes only, 1 retention day |
| Opt-in secure URLs | aus |
| Fallback voice id | automatic fallback |
| Default dynamic variables | keine |

## Webhook Settings

Über Webhooks sendet Retell anrufbezogene Events (z. B. Anruf gestartet/beendet, Auswertung fertig) an eine von euch konfigurierte URL — so kann unser Backend automatisch darauf reagieren. Einstellbar sind:

- **Agent Level Webhook URL:** Ziel-URL, an die Retell die Events sendet.
- **Webhook Timeout:** maximale Wartezeit auf eine Webhook-Antwort, bevor abgebrochen wird.
- **Webhook Events:** Auswahl, welche Ereignisse dieser Webhook erhalten soll — z. B. _Chat started_, _Chat ended_, _Transcript updated_, _Chat analyzed_ (bei Voice-Agenten entsprechend die Call-Events).

**Trends4Markets-Default:**

- Agent level webhook URL: `backend.Trends4Markets`-URL einfügen.
- Andere Einstellungen auf Standard lassen.

## MCP Settings

Über **MCP (Model Context Protocol)** bindet ihr einen **externen MCP-Server an den Agenten** an, sodass dieser dessen Tools/Funktionen während des Gesprächs nutzen kann. MCP ist dabei nur eine standardisierte Schnittstelle zu Funktionen — vergleichbar mit Custom Functions, aber über einen MCP-Server bereitgestellt.

!!! note "Nicht verwechseln" Hier geht es darum, dem Agenten einen externen MCP-Server hinzuzufügen. Davon zu unterscheiden ist Retells _eigener_ MCP-Server (`https://mcp.retellai.com`), mit dem man umgekehrt die Retell-Plattform aus KI-Clients wie Cursor, Claude Desktop oder Claude Code **steuert**.

**Add-MCP-Dialog — Felder:**

![Add-MCP-Dialog in Retell](/images/retell/retell-mcp-add.png)

- **Name:** Name des MCP-Servers im Workspace.
- **URL:** Endpunkt-URL des MCP-Servers.
- **Timeout (ms):** maximale Wartezeit pro Anfrage (Default 10000 ms = 10 s).
- **Headers:** HTTP-Header für die Verbindung als Key-Value-Paare (z. B. `Authorization: Bearer <TOKEN>`).
- **Query Parameters:** Query-String-Parameter, die an die URL angehängt werden, als Key-Value-Paare.

**Sicherheitshinweise** (gelten allgemein für MCP):

- Ein MCP gibt dem Agenten Zugriff auf externe Tools — wie das Erteilen von Betriebsrechten. **Least Privilege:** nur die nötigen Rechte/Keys vergeben.
- **API-Keys gehören in die Header/Secrets**, nicht in Prompts.
- **Prompt-Injection-Risiko:** Untrusted Content (Transkripte, Nutzereingaben, KB-Dokumente) kann Anweisungen enthalten, die das Modell zu ungewollten Aktionen verleiten — destruktive Aktionen absichern.
- Vorsicht mit PII in Logs/Transkripten.

Allgemeine MCP-/Sicherheitsinfos zusammengefasst aus der Retell-Doku „Retell MCP server for AI assistants" (`https://docs.retellai.com`); Feldbeschreibungen aus dem Add-MCP-Dialog.

**Trends4Markets-Default:**

Vorläufig keine festen Defaults, da die Konfiguration stark kundenabhängig ist.