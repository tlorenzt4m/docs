---
title: "Retell-Funktionen & Custom Functions"
audience: ["prompt_engineer", "admin"]
product: "intern"
module: "retell"
route: "/retell/funktionen"
tags: ["retell", "funktionen", "custom-functions", "api", "transfer"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Retell-Funktionen & Custom Functions

## Was ist das?

Der Funktionsknoten wird verwendet, um innerhalb eines Gesprächsflusses (Conversation Flow) entweder vorgefertigte oder benutzerdefinierte Funktionen aufzurufen.

- **Ablauf:** Sobald der Agent den Knoten erreicht, wird die Funktion ausgeführt. Basierend auf dem Ergebnis erfolgt der Übergang (Transition) zum nächsten Schritt im Flow.
- **Zweck:** Technische Logik, nicht direkte Konversation – auch wenn der Agent während der Ausführung sprechen kann.

Verfügbare Typen: Benutzerdefinierte Funktionen (Custom Functions) oder vorgefertigte Funktionen wie Kalenderprüfung oder Terminbuchung.

## Schritte (Retell-Übersicht)

1. **Funktionen hinzufügen:** Bevor eine Funktion in einem Knoten genutzt werden kann, muss sie zuerst im System angelegt werden.
2. **Timing des Übergangs (Transition):** Hängt von zwei Hauptfaktoren ab:
   - **Wait for Result DEAKTIVIERT:** Der Agent wechselt sofort nach dem Funktionsaufruf zum nächsten Knoten (oder sobald er zu Ende gesprochen hat).
   - **Wait for Result AKTIVIERT:** Der Agent wartet, bis die Funktion fertig ausgeführt wurde. So ist das Ergebnis im nächsten Knoten sofort verfügbar.
3. **Wichtige Knoteneinstellungen:**
   - **Speak During Execution:** Was der Agent sagen soll, während die Funktion läuft (z. B. „Einen Moment, ich schaue kurz nach …").
   - **Wait for Result:** Agent wartet auf die vollständige Ausführung, bevor er den Knoten wechselt.
   - **Global Node:** Markiert den Knoten als global.
   - **Block Interruptions:** Nutzer kann den Agenten nicht unterbrechen, während dieser im Funktionsknoten spricht.
   - **LLM-Auswahl:** Für diesen Knoten kann ein anderes Sprachmodell gewählt werden (z. B. für präzisere Funktionsargumente).
   - **Fine-tuning Examples:** Übergang zwischen Knoten per Beispielen präzise anpassen.
4. **Ergebnis-Übermittlung an den Nutzer:** Da der Funktionsknoten selbst keine Unterhaltung führt, im Anschluss einen Konversationsknoten (Conversation Node) verknüpfen.

!!! tip Verschiedene Konversationsknoten für unterschiedliche Funktionsergebnisse erstellen (z. B. „Termin erfolgreich gebucht" und „Termin leider bereits belegt").

## Custom Functions (Benutzerdefinierte Funktionen)

Benutzerdefinierte Funktionen erweitern die Fähigkeiten eines Agenten, indem während eines Telefonats externe APIs aufgerufen werden – um zusätzliches Wissen bereitzustellen, externe Logik zu implementieren oder Aktionen in Drittsystemen auszuführen.

![Custom Functions in Retell](/images/retell/retell-custom-function.png)

### Schritte zur Erstellung

Wenn eine Funktion aufgerufen wird, sendet Retell eine HTTP-Anfrage an eine festgelegte URL.

1. **Konfiguration der Details:** Eindeutiger Name (mit Unterstrichen, z. B. `get_user_details`) und Beschreibung, damit das LLM weiß, wann die Funktion zu nutzen ist.
2. **HTTP-Methode wählen:** GET, POST, PATCH, PUT oder DELETE.
3. **Endpoint-URL:** Zieladresse, an die Retell die Anfrage sendet.
4. **Header und Query-Parameter (optional):** Statisch oder mit dynamischen Variablen. Query-Parameter als fester Wert (`const`) oder als Beschreibung (vom LLM ausgefüllt).
5. **Parameter definieren:** Für POST/PATCH/PUT via JSON-Schema.
6. **Option „Payload: args only":** Aktiviert → nur das Argument-Objekt (flacher JSON-Body). Deaktiviert → Body enthält zusätzlich Metadaten wie Funktionsname und Anruf-Details.
7. **Antwortvariablen festlegen (optional):** Werte aus der API-Antwort extrahieren und als dynamische Variablen (z. B. `user_name`) speichern.

### Technische Spezifikationen (Request & Response)

- **Request – Header:** Enthält `X-Retell-Signature` zur Verifizierung und `Content-Type: application/json`.
- **Request – Body:** Standardmäßig Funktionsname (`name`), Anruf-Objekt (`call`, inkl. Echtzeit-Transkript) und Argumente (`args`).
- **Response:** Statuscode 200–299 signalisiert Erfolg. Formate String, JSON oder Buffer möglich; Retell wandelt alles in einen String für das LLM. Ergebnis auf **15.000 Zeichen** begrenzt.

### Sicherheit und Fehlerbehebung

- **Verifizierung:** Über den `X-Retell-Signature`-Header sicherstellen, dass die Anfrage von Retell kommt.
- **IP-Allowlisting:** Zugriff auf die Retell-IP `100.20.5.228` beschränken.
- **Fehlerbehebung:** Häufig ein ungültiges JSON-Schema (oft fehlt `"type": "object"` auf oberster Ebene). Bei Fehlern bis zu zwei automatische Wiederholungsversuche.

## Trends4Markets-Default (Function-Einstellungen)

| Einstellung | Wert |
| --- | --- |
| Parameters im JSON | `partnerID` muss mit der `partnerID` im Backend übereinstimmen |
| `transfer_call_variable` | Description definiert, wann was gemacht werden soll |
| Transfer to | **dynamic routing** mit `"{{number}}"` einfügen |
| Wie handhabt die AI den Transfer? | **Cold Transfer** |
| SIP Transfer Method | **SIP invite** |
| Displayed Caller ID | **Retell Agent's Numbers** (nicht die User-Nummer) |
| Transfer Ring Duration | 20 sec |
| Talk while waiting | „Einen Moment bitte, ich stelle euch durch." |

## Häufige Probleme

| Problem | Lösung |
| --- | --- |
| Funktion wird nicht aufgerufen | Name und Beschreibung prüfen, damit das LLM den Einsatz erkennt |
| HTTP-Fehler / kein Ergebnis | JSON-Schema prüfen (`"type": "object"` oben), Endpoint-URL und Header kontrollieren |
| Transfer landet bei falscher Nummer | `transfer_call_variable` und dynamic routing `{{number}}` prüfen |