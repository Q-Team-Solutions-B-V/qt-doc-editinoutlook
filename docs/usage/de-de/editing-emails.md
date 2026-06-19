# E-Mails bearbeiten

Auf dieser Seite wird beschrieben, wie Sie Edit in Outlook verwenden, um E-Mails zu Business Central-Dokumenten über Microsoft Outlook zu bearbeiten und zu versenden.

## Grundlegender Workflow

### Schritt-für-Schritt-Prozess

#### 1. Dokumentauswahl
1. **Öffnen Sie ein Business Central-Dokument** (z. B. Verkaufsangebot, Rechnung, Auftrag)
2. **Klicken Sie auf „E-Mail senden"** im Menüband
3. **Das E-Mail-Dialogfeld wird geöffnet**

#### 2. Edit in Outlook aktivieren
1. **Im E-Mail-Dialogfeld**:
   - Empfänger auswählen
   - E-Mail-Vorlage auswählen (optional)
   - **Auf „In Outlook bearbeiten"** klicken
2. **Der Browser startet den Download** der .eml-Datei
3. **Warten Sie, bis der Download abgeschlossen ist**

#### 3. Bearbeiten in Outlook
1. **Öffnen Sie die heruntergeladene .eml-Datei** (Doppelklick)
2. **Outlook öffnet sich** mit einer vorausgefüllten E-Mail:
   - Dokument als PDF-Anhang
   - Vorlageninhalt im E-Mail-Text
   - Empfängerinformationen ausgefüllt
3. **Bearbeiten Sie die E-Mail** nach Belieben:
   - Betreffzeile anpassen
   - Persönlichen Text hinzufügen
   - Weitere Anhänge hinzufügen
   - Formatierung anpassen

#### 4. Senden
1. **E-Mail überprüfen**
2. **Auf „Senden"** in Outlook klicken
3. **E-Mail wird gesendet** über Ihr persönliches Outlook-Konto
4. **E-Mail erscheint** in Ihrem Outlook-Ordner „Gesendete Elemente"

## Unterstützte Dokumente

### Verkaufsdokumente
| Dokumenttyp | Business Central-Seite | Verfügbare Aktionen |
|-------------|------------------------|---------------------|
| **Verkaufsangebote** | Verkaufsangebot (41, 42, 43) | E-Mail senden → In Outlook bearbeiten |
| **Verkaufsaufträge** | Verkaufsauftrag (44, 45, 46) | E-Mail senden → In Outlook bearbeiten |
| **Verkaufsrechnungen** | Verkaufsrechnung (132, 133, 134) | E-Mail senden → In Outlook bearbeiten |
| **Gebuchte Verkaufsrechnungen** | Gebuchte Verkaufsrechnung (132) | E-Mail senden → In Outlook bearbeiten |
| **Verkaufsgutschriften** | Verkaufsgutschrift (114, 115) | E-Mail senden → In Outlook bearbeiten |

### Einkaufsdokumente
| Dokumenttyp | Business Central-Seite | Verfügbare Aktionen |
|-------------|------------------------|---------------------|
| **Einkaufsangebote** | Einkaufsangebot (49, 50, 51) | E-Mail senden → In Outlook bearbeiten |
| **Einkaufsbestellungen** | Einkaufsbestellung (52, 53, 54) | E-Mail senden → In Outlook bearbeiten |
| **Einkaufsrechnungen** | Einkaufsrechnung (122, 123, 124) | E-Mail senden → In Outlook bearbeiten |
| **Einkaufsgutschriften** | Einkaufsgutschrift (124, 125) | E-Mail senden → In Outlook bearbeiten |

### Lagerdokumente
| Dokumenttyp | Business Central-Seite | Verfügbare Aktionen |
|-------------|------------------------|---------------------|
| **Lagerlieferungen** | Lagerlieferung (7337) | E-Mail senden → In Outlook bearbeiten |
| **Gebuchte Lagerlieferungen** | Gebuchte Lagerlieferung (7348) | E-Mail senden → In Outlook bearbeiten |

## Benutzeroberfläche

### Business Central-E-Mail-Dialogfeld
Wenn Sie „E-Mail senden" auswählen, sehen Sie:

![Business Central-Dialogfeld „E-Mail senden“](../../assets/Send%20Email.png)

### Download-Aufforderung für Edit in Outlook
Nach dem Klicken auf „In Outlook bearbeiten":

![Download](../../assets/Download.png)

### Outlook-Verfassensfenster
Die .eml-Datei öffnet sich in Outlook mit:

```
┌─ Neue Nachricht - Outlook ──────────────────┐
│ Von: ihre-email@unternehmen.de              │
│ An: kunde@beispiel.de                       │
│ Betreff: Verkaufsangebot VA001              │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Sehr geehrte Damen und Herren,          │ │
│ │                                         │ │
│ │ anbei erhalten Sie unser Angebot VA001. │ │
│ │                                         │ │
│ │ Mit freundlichen Grüßen,               │ │
│ │ [Ihr Name]                              │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Anhänge: 📎 Verkaufsangebot_VA001.pdf     │
│                                             │
│ [Senden] [Entwurf speichern] [Verwerfen]   │
└─────────────────────────────────────────────┘
```

## E-Mail-Bearbeitungsfunktionen

### Textanpassungen
In Outlook können Sie:
- **Betreffzeile ändern**
- **E-Mail-Text anpassen**:
  - Persönliche Notiz hinzufügen
  - Vorlagentext ändern
  - Formatierung anpassen (fett, kursiv, Farben)
  - Listen hinzufügen
  - Links einfügen

### Anlagenverwaltung
- **Vorhandene Anhänge anzeigen** (PDF-Dokument)
- **Weitere Anhänge hinzufügen**:
  - Zusätzliche Dokumente
  - Bilder
  - Spezifikationen
  - Verträge
- **Anhänge entfernen** (falls erforderlich)
- **Anhänge umbenennen**

### Empfänger anpassen
- **An-Feld erweitern** mit weiteren Empfängern
- **Cc-Empfänger hinzufügen**
- **Bcc für verdeckte Kopien**
- **Adressen validieren** über das Outlook-Adressbuch

### Signatur & Formatierung
- **Persönliche Signatur** wird automatisch hinzugefügt
- **Unternehmensdesign** aus Vorlage beibehalten
- **HTML-Formatierung** vollständig verfügbar
- **Rich-Text-Bearbeitung** mit dem Outlook-Editor

## Erweiterte Funktionen

### Vorlagenpersonalisierung
Vorlagen situationsgerecht anpassen:

```html
<!-- Vor dem Senden -->
<p>Sehr geehrte/r %CUSTOMER_NAME%,</p>
<p>anbei erhalten Sie %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Nach der Bearbeitung in Outlook -->
<p>Sehr geehrter Herr Müller,</p>
<p>im Anschluss an unser heutiges Gespräch erhalten Sie anbei
unser überarbeitetes Verkaufsangebot VA001 mit den aktualisierten Preisen.</p>
```

### Massen-E-Mail-Bearbeitung
Für mehrere Dokumente:
1. **Edit in Outlook verwenden** für das erste Dokument
2. **Als Vorlage speichern** in Outlook
3. **Vorlage anwenden** für nachfolgende Dokumente
4. **Jede Nachricht personalisieren**

**Siehe auch:** [Unterstützte Versionen](supported-versions.md) | [Einschränkungen](limitations.md)
