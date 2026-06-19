# Redigering af e-mails

Denne side beskriver, hvordan du bruger Edit in Outlook til at redigere og sende e-mails til Business Central-dokumenter via Microsoft Outlook.

## Grundlæggende arbejdsgang

### Trin-for-trin-proces

#### 1. Dokumentvalg
1. **Åbn et Business Central-dokument** (f.eks. salgstilbud, faktura, ordre)
2. **Klik på „Send e-mail"** i båndet
3. **E-mail-dialogboksen åbnes**

#### 2. Aktivér Edit in Outlook
1. **I e-mail-dialogboksen**:
   - Vælg modtagere
   - Vælg en e-mailskabelon (valgfrit)
   - **Klik på „Rediger i Outlook"**
2. **Browseren starter download** af .eml-filen
3. **Vent, til download er fuldført**

#### 3. Redigering i Outlook
1. **Åbn den downloadede .eml-fil** (dobbeltklik)
2. **Outlook åbner** med en forudfyldt e-mail:
   - Dokument som PDF-vedhæftning
   - Skabelonindhold i e-mail-brødteksten
   - Modtagerinformation udfyldt
3. **Rediger e-mailen** efter behov:
   - Juster emnelinjen
   - Tilføj personlig tekst
   - Tilføj ekstra vedhæftninger
   - Juster formatering

#### 4. Afsendelse
1. **Gennemgå din e-mail**
2. **Klik på „Send"** i Outlook
3. **E-mailen sendes** via din personlige Outlook-konto
4. **E-mailen vises** i din Outlook-mappe „Sendte elementer"

## Understøttede dokumenter

### Salgsdokumenter
| Dokumenttype | Business Central-side | Tilgængelige handlinger |
|--------------|----------------------|------------------------|
| **Salgstilbud** | Salgstilbud (41, 42, 43) | Send e-mail → Rediger i Outlook |
| **Salgsordrer** | Salgsordre (44, 45, 46) | Send e-mail → Rediger i Outlook |
| **Salgsfakturaer** | Salgsfaktura (132, 133, 134) | Send e-mail → Rediger i Outlook |
| **Bogførte salgsfakturaer** | Bogført salgsfaktura (132) | Send e-mail → Rediger i Outlook |
| **Salgskreditnotaer** | Salgskreditnota (114, 115) | Send e-mail → Rediger i Outlook |

### Indkøbsdokumenter
| Dokumenttype | Business Central-side | Tilgængelige handlinger |
|--------------|----------------------|------------------------|
| **Indkøbstilbud** | Indkøbstilbud (49, 50, 51) | Send e-mail → Rediger i Outlook |
| **Indkøbsordrer** | Indkøbsordre (52, 53, 54) | Send e-mail → Rediger i Outlook |
| **Indkøbsfakturaer** | Indkøbsfaktura (122, 123, 124) | Send e-mail → Rediger i Outlook |
| **Indkøbskreditnotaer** | Indkøbskreditnota (124, 125) | Send e-mail → Rediger i Outlook |

### Lagerdokumenter
| Dokumenttype | Business Central-side | Tilgængelige handlinger |
|--------------|----------------------|------------------------|
| **Lagerleverancer** | Lagerleverance (7337) | Send e-mail → Rediger i Outlook |
| **Bogførte lagerleverancer** | Bogført lagerleverance (7348) | Send e-mail → Rediger i Outlook |

## Brugergrænseflade

### Business Central-e-mail-dialogboks
Når du vælger „Send e-mail", ser du:

```
┌─ E-mailbesked ──────────────────────────────┐
│ Til: kunde@eksempel.dk                      │
│ Cc:                                         │
│ Bcc:                                        │
│ Emne: Salgstilbud ST001                     │
│                                             │
│ Skabelon: [Vælg skabelon ▼]               │
│ Vedhæftning: Salgstilbud ST001.pdf ☑      │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ [Rediger i Outlook] [Send direkte]      │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [OK] [Annuller]                             │
└─────────────────────────────────────────────┘
```

### Download-prompt for Edit in Outlook
Efter klik på „Rediger i Outlook":

```
┌─ Browser-download ──────────────────────────┐
│ ⬇ Downloader: Salgstilbud_ST001.eml       │
│                                             │
│ ✓ Download fuldført                        │
│                                             │
│ [ Åbn med Outlook ]  [ Vis i mappe ]       │
└─────────────────────────────────────────────┘
```

### Outlook-skrivevindue
.eml-filen åbnes i Outlook med:

```
┌─ Ny besked - Outlook ───────────────────────┐
│ Fra: din-email@virksomhed.dk               │
│ Til: kunde@eksempel.dk                      │
│ Emne: Salgstilbud ST001                     │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Kære kunde,                             │ │
│ │                                         │ │
│ │ Vedlagt finder du vores tilbud ST001.  │ │
│ │                                         │ │
│ │ Med venlig hilsen,                     │ │
│ │ [Dit navn]                              │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Vedhæftninger: 📎 Salgstilbud_ST001.pdf  │
│                                             │
│ [Send] [Gem kladde] [Kassér]               │
└─────────────────────────────────────────────┘
```

## Funktioner til redigering af e-mails

### Tekstjusteringer
I Outlook kan du:
- **Ændre emnelinjen**
- **Justere brødteksten**:
  - Tilføje en personlig note
  - Ændre skabelonteksten
  - Justere formatering (fed, kursiv, farver)
  - Tilføje lister
  - Indsætte links

### Håndtering af vedhæftninger
- **Se eksisterende vedhæftninger** (PDF-dokument)
- **Tilføje ekstra vedhæftninger**:
  - Yderligere dokumenter
  - Billeder
  - Specifikationer
  - Kontrakter
- **Fjerne vedhæftninger** (om nødvendigt)
- **Omdøbe vedhæftninger**

### Justering af modtagere
- **Udvide Til-feltet** med yderligere modtagere
- **Tilføje Cc-modtagere**
- **Bcc for skjulte kopier**
- **Validere adresser** via Outlook-adressebogen

### Signatur og formatering
- **Personlig signatur** tilføjes automatisk
- **Virksomhedsbranding** bevaret fra skabelon
- **HTML-formatering** fuldt tilgængeligt
- **Tekstbehandling med formatering** via Outlook-editoren

## Avancerede funktioner

### Tilpasning af skabelon
Tilpas skabeloner til situationen:

```html
<!-- Før afsendelse -->
<p>Kære %CUSTOMER_NAME%,</p>
<p>Vedlagt finder du %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Efter redigering i Outlook -->
<p>Kære Jens Hansen,</p>
<p>I forlængelse af vores samtale i dag finder du vedlagt
vores reviderede salgstilbud ST001 med de opdaterede priser.</p>
```

### Masseopredigering af e-mails
For flere dokumenter:
1. **Brug Edit in Outlook** til det første dokument
2. **Gem som skabelon** i Outlook
3. **Anvend skabelon** på efterfølgende dokumenter
4. **Personaliser** hver besked

**Se også:** [Understøttede versioner](supported-versions.md) | [Begrænsninger](limitations.md)
