# Redigere e-poster

Denne siden beskriver hvordan du bruker Edit in Outlook til å redigere og sende e-poster til Business Central-dokumenter via Microsoft Outlook.

## Grunnleggende arbeidsflyt

### Trinn-for-trinn-prosess

#### 1. Dokumentvalg
1. **Åpne et Business Central-dokument** (f.eks. salgstilbud, faktura, ordre)
2. **Klikk på «Send e-post»** i båndet
3. **E-post-dialogboksen åpnes**

#### 2. Aktiver Edit in Outlook
1. **I e-post-dialogboksen**:
   - Velg mottakere
   - Velg en e-postmal (valgfritt)
   - **Klikk på «Rediger i Outlook»**
2. **Nettleseren starter nedlasting** av .eml-filen
3. **Vent til nedlastingen er fullført**

#### 3. Redigering i Outlook
1. **Åpne den nedlastede .eml-filen** (dobbeltklikk)
2. **Outlook åpnes** med en forhåndsutfylt e-post:
   - Dokument som PDF-vedlegg
   - Malinnhold i e-postteksten
   - Mottakerinformasjon utfylt
3. **Rediger e-posten** etter behov:
   - Juster emnelinjen
   - Legg til personlig tekst
   - Legg til ekstra vedlegg
   - Juster formatering

#### 4. Sending
1. **Gjennomgå e-posten**
2. **Klikk på «Send»** i Outlook
3. **E-posten sendes** via din personlige Outlook-konto
4. **E-posten vises** i Outlook-mappen «Sendte elementer»

## Støttede dokumenter

### Salgsdokumenter
| Dokumenttype | Business Central-side | Tilgjengelige handlinger |
|--------------|----------------------|-------------------------|
| **Salgstilbud** | Salgstilbud (41, 42, 43) | Send e-post → Rediger i Outlook |
| **Salgsordrer** | Salgsordre (44, 45, 46) | Send e-post → Rediger i Outlook |
| **Salgsfakturaer** | Salgsfaktura (132, 133, 134) | Send e-post → Rediger i Outlook |
| **Bokførte salgsfakturaer** | Bokført salgsfaktura (132) | Send e-post → Rediger i Outlook |
| **Salgskreditnotaer** | Salgskreditnota (114, 115) | Send e-post → Rediger i Outlook |

### Innkjøpsdokumenter
| Dokumenttype | Business Central-side | Tilgjengelige handlinger |
|--------------|----------------------|-------------------------|
| **Innkjøpstilbud** | Innkjøpstilbud (49, 50, 51) | Send e-post → Rediger i Outlook |
| **Innkjøpsordrer** | Innkjøpsordre (52, 53, 54) | Send e-post → Rediger i Outlook |
| **Innkjøpsfakturaer** | Innkjøpsfaktura (122, 123, 124) | Send e-post → Rediger i Outlook |
| **Innkjøpskreditnotaer** | Innkjøpskreditnota (124, 125) | Send e-post → Rediger i Outlook |

### Lagerdokumenter
| Dokumenttype | Business Central-side | Tilgjengelige handlinger |
|--------------|----------------------|-------------------------|
| **Lagerforsendelser** | Lagerforsendelse (7337) | Send e-post → Rediger i Outlook |
| **Bokførte lagerforsendelser** | Bokført lagerforsendelse (7348) | Send e-post → Rediger i Outlook |

## Brukergrensesnitt

### Business Central-e-post-dialogboks
Når du velger «Send e-post», ser du:

```
┌─ E-postmelding ─────────────────────────────┐
│ Til: kunde@eksempel.no                      │
│ Kopi:                                       │
│ Blindkopi:                                  │
│ Emne: Salgstilbud ST001                     │
│                                             │
│ Mal: [Velg mal ▼]                          │
│ Vedlegg: Salgstilbud ST001.pdf ☑           │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ [Rediger i Outlook] [Send direkte]      │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [OK] [Avbryt]                               │
└─────────────────────────────────────────────┘
```

### Nedlastingsforespørsel for Edit in Outlook
Etter klikk på «Rediger i Outlook»:

```
┌─ Nettlesernedlasting ───────────────────────┐
│ ⬇ Laster ned: Salgstilbud_ST001.eml       │
│                                             │
│ ✓ Nedlasting fullført                      │
│                                             │
│ [ Åpne med Outlook ]  [ Vis i mappe ]      │
└─────────────────────────────────────────────┘
```

### Outlook-skrivevindu
.eml-filen åpnes i Outlook med:

```
┌─ Ny melding - Outlook ──────────────────────┐
│ Fra: din-epost@bedrift.no                   │
│ Til: kunde@eksempel.no                      │
│ Emne: Salgstilbud ST001                     │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Kjære kunde,                            │ │
│ │                                         │ │
│ │ Vedlagt finner du vårt tilbud ST001.   │ │
│ │                                         │ │
│ │ Med vennlig hilsen,                    │ │
│ │ [Ditt navn]                             │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Vedlegg: 📎 Salgstilbud_ST001.pdf         │
│                                             │
│ [Send] [Lagre utkast] [Forkast]            │
└─────────────────────────────────────────────┘
```

## Funksjoner for e-postredigering

### Tekstjusteringer
I Outlook kan du:
- **Endre emnelinjen**
- **Justere brødteksten**:
  - Legge til en personlig merknad
  - Endre malteksten
  - Justere formatering (fet, kursiv, farger)
  - Legge til lister
  - Sette inn lenker

### Vedleggsbehandling
- **Vise eksisterende vedlegg** (PDF-dokument)
- **Legge til ekstra vedlegg**:
  - Ytterligere dokumenter
  - Bilder
  - Spesifikasjoner
  - Kontrakter
- **Fjerne vedlegg** (om nødvendig)
- **Gi vedlegg nytt navn**

### Justere mottakere
- **Utvide Til-feltet** med flere mottakere
- **Legge til Kopi-mottakere**
- **Blindkopi for skjulte kopier**
- **Validere adresser** via Outlook-adresseboken

### Signatur og formatering
- **Personlig signatur** legges til automatisk
- **Bedriftsprofil** beholdt fra mal
- **HTML-formatering** fullt tilgjengelig
- **Rik tekstredigering** med Outlook-editoren

## Avanserte funksjoner

### Malpersonalisering
Tilpass maler til situasjonen:

```html
<!-- Før sending -->
<p>Kjære %CUSTOMER_NAME%,</p>
<p>Vedlagt finner du %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Etter redigering i Outlook -->
<p>Kjære Per Hansen,</p>
<p>I forlengelse av vår samtale i dag finner du vedlagt
vårt reviderte salgstilbud ST001 med de oppdaterte prisene.</p>
```

### Masseredigering av e-poster
For flere dokumenter:
1. **Bruk Edit in Outlook** for det første dokumentet
2. **Lagre som mal** i Outlook
3. **Bruk malen** på påfølgende dokumenter
4. **Personaliser** hver melding

**Se også:** [Støttede versjoner](supported-versions.md) | [Begrensninger](limitations.md)
