---
title: "Trends4Markets Prompt-Standard"
audience: ["prompt_engineer"]
product: "intern"
module: "retell"
route: "/retell/prompt-standard"
tags: ["retell", "prompt", "standard", "framework"]
visibility: "internal"
version: "2026-06"
doc_status: "published"
---

# Trends4Markets Prompt-Standard

## Was ist das?

Die einheitliche Grundstruktur, nach der wir Voice-Agent-Prompts aufbauen.

## Wofür brauchen wir das?

Damit alle Prompts konsistent, vollständig und wartbar sind – unabhängig davon, wer sie schreibt.

## Framework-Prompt-Grundstruktur

Zum Kopieren & Einfügen:

```text
## Identität & Rolle
## Wissen / Kontext
## Aufgabe
## Regeln / Instruktionen / Sonderregeln
## Aussprache / Stil oder Text-to-Speech Guidelines
## Grenzen / Restriktionen
```

## Erklärung der Abschnitte

| Abschnitt | Inhalt |
| --- | --- |
| `## Identität & Rolle` | Was der AI-Agent ist und in welchem Kontext er agiert: Funktion (z. B. Telefonassistenz) und Position im Unternehmen (z. B. First-Level-Support). |
| `## Wissen / Kontext` | Auf welche Informationsgrundlage die KI zugreifen darf: Verweis auf die zu nutzenden Quellen für Fachfragen, z. B. die interne Knowledge Base. |
| `## Aufgabe` | Das Hauptziel des Gesprächs: Kernaktivität, z. B. Anfragen bearbeiten, Informationen bereitstellen, das Gespräch aktiv und responsiv führen. |
| `## Regeln / Instruktionen / Sonderregeln` | Spezifische Verhaltensanweisungen: Etikette (z. B. konsequentes Siezen, Umgang mit Namen) und Gesprächsdynamik. |
| `## Aussprache / Stil oder Text-to-Speech Guidelines` | Tonalität und sprachliche Optimierung: Klangbild (z. B. natürlich, alltäglich) sowie technische Hinweise für besseren Redefluss. |
| `## Grenzen / Restriktionen` | Klare Verbote oder Limitierungen: formale Einschränkungen, z. B. Begrenzung der Antwortlänge auf maximal zwei Sätze. |

## Praxisbeispiele für Sonderregeln

Konkrete, bewährte Formulierungen für den Abschnitt `## Regeln / Instruktionen / Sonderregeln`.

### Passives Zuhören (z. B. Außendienstbericht)

**Anwendungsfall:** Der Nutzer möchte einen längeren Bericht am Stück einsprechen (z. B. Außendienstbericht), ohne dass der Agent zwischendurch nachfragt oder das Gespräch unterbricht. Der Agent soll erst zuhören, bis der Nutzer fertig ist, und danach das Gesagte vollständig transkribieren/weiterverarbeiten.

**Lösung:** Im Systemprompt folgende Anweisung ergänzen:

```text
NO_RESPONSE_NEEDED
```

Damit hält sich der Agent während der Berichtsaufnahme mit Rückfragen und Zwischenantworten zurück und lässt den Nutzer ungestört durchsprechen.

### Widerspruch gegen die Gesprächsaufzeichnung

**Anwendungsfall:** Der Anrufer widerspricht der Aufzeichnung des Gesprächs oder akzeptiert die Datenschutzbestimmungen nicht.

**Lösung:** Im Systemprompt folgende Regel ergänzen:

```text
Widerspricht der Kunde der Aufzeichnung, nenne Website oder Filiale als alternative Kontaktwege. Bestätige ein Stoppen der Aufzeichnung mündlich, es erfolgt technisch tatsächlich im Nachgang.
```

Der Widerspruch wird zusätzlich über das Post-Call-Extraktionsfeld `custom_deny_consent` erfasst (siehe [Weitere Einstellungen → Post-Call Data Extraction](/intern/retell/weitere-einstellungen#post-call-data-extraction)), damit die Aufzeichnung im Nachgang technisch entsprechend behandelt wird.

## Ergebnis prüfen

- Alle sechs Abschnitte sind im Prompt vorhanden und gefüllt.
- Anweisungen stehen im Prompt – nicht in der Knowledge Base.