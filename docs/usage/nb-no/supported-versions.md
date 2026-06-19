# Støttede versjoner

Denne siden gir en oversikt over alle støttede versjoner og kompatibilitet for Edit in Outlook.

## Business Central-versjoner

### Gjeldende støtte

#### Business Central SaaS
| BC-versjon | Edit in Outlook-versjon | Status | Utgivelsesdato | EOL-dato |
|-----------|------------------------|--------|----------------|---------|
| **BC 27** | 27.0.46066.0+ | ✅ Gjeldende | November 2024 | April 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Støttet | April 2024 | Oktober 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Støttet | Oktober 2023 | April 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Eldre | April 2023 | Oktober 2024 |

#### Business Central lokal installasjon
| BC-versjon | Edit in Outlook-versjon | Status | Merknader |
|-----------|------------------------|--------|----------|
| **BC 27** | 27.0.46066.0+ | ✅ Gjeldende | Full funksjonalitet |
| **BC 26** | 26.0.45889.0+ | ✅ Støttet | Full funksjonalitet |
| **BC 25** | 25.0.45294.0+ | ✅ Støttet | Begrensede nye funksjoner |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Eldre | Bare sikkerhetsoppdateringer |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Ikke lenger støttet |

### Eldre versjoner (Separate repositorier)
For eldre Business Central-versjoner er spesifikke eldre versjoner tilgjengelige:

#### BC 16 (2020 Wave 1)
- **Repositorium**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Siste versjon**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repositorium**: `qt-bc-outlookedit-legacy-15`
- **Status**: ❌ End of Life
- **Siste versjon**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repositorium**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life
- **Siste versjon**: 14.0.xxxxx.0

## Microsoft Office-versjoner

### Office 365 / Microsoft 365

#### Outlook Desktop
| Versjon | Status | Merknader |
|---------|--------|----------|
| **Outlook 365 Gjeldende** | ✅ Fullt støttet | Anbefalt plattform |
| **Outlook 365 Semi-Annual** | ✅ Støttet | Stabil bedriftsversjon |
| **Outlook 2021 LTSC** | ✅ Støttet | Lokal bedriftsversjon |
| **Outlook 2019** | ⚠️ Begrenset støtte | Grunnleggende funksjonalitet |
| **Outlook 2016** | ❌ Ikke støttet | For gammel for EML |

#### Outlook Web Access (OWA)
| Versjon | Status | EML-støtte | Merknader |
|---------|--------|-----------|----------|
| **OWA Gjeldende** | ✅ Støttet | Via nedlasting | Nettleseravhengig |
| **OWA Government** | ✅ Støttet | Via nedlasting | Samsvarsgodkjent |

#### Outlook Mobile
| Plattform | Status | Funksjonalitet |
|-----------|--------|---------------|
| **iOS Outlook** | ✅ Støttet | Via fildeling |
| **Android Outlook** | ✅ Støttet | Via fildeling |
| **Windows Mobile** | ❌ Ikke støttet | Plattform avviklet |

### Office lokal installasjon
| Versjon | Status | Installasjon | Merknader |
|---------|--------|-------------|----------|
| **Office LTSC 2021** | ✅ Støttet | MSI/Click-to-Run | Anbefalt for bedrifter |
| **Office 2019** | ⚠️ Begrenset | MSI/Click-to-Run | Grunnleggende EML-støtte |
| **Office 2016** | ❌ Ikke støttet | - | EOL nådd |

## Nettleserkompatibilitet

### Anbefalte nettlesere

#### Windows
| Nettleser | Versjon | Status | Ytelse |
|-----------|---------|--------|--------|
| **Microsoft Edge** | 118+ | ✅ Utmerket | Beste ytelse |
| **Chrome** | 118+ | ✅ Utmerket | Meget god ytelse |
| **Firefox** | 118+ | ✅ God | God ytelse |
| **Internet Explorer** | Alle | ❌ Ikke støttet | Avviklet |

#### macOS
| Nettleser | Versjon | Status | Ytelse |
|-----------|---------|--------|--------|
| **Safari** | 16+ | ✅ God | Innebygd macOS-integrering |
| **Chrome** | 118+ | ✅ Utmerket | Konsistens på tvers av plattformer |
| **Firefox** | 118+ | ✅ God | Åpen kildekode-alternativ |
| **Edge** | 118+ | ✅ Utmerket | Microsoft-økosystem |

### Control Add-in-krav
- **JavaScript**: ES6+-støtte
- **HTML5**: Canvas og File API
- **CSS3**: Flexbox- og Grid-oppsett
- **WebAssembly**: For PDF-forhåndsvisning (valgfritt)

## Plattformstøtte

### Operativsystemer

#### Windows
| Versjon | Status | Outlook-integrering | Merknader |
|---------|--------|--------------------| --------- |
| **Windows 11** | ✅ Fullt støttet | Innebygd | Anbefalt plattform |
| **Windows 10 (1909+)** | ✅ Støttet | Innebygd | Minimumsversjon |
| **Windows Server 2022** | ✅ Støttet | Terminal Server | Bedriftsscenario |
| **Windows Server 2019** | ✅ Støttet | Terminal Server | Eldre bedrift |
| **Windows 8.1** | ❌ Ikke støttet | - | EOL nådd |

#### macOS
| Versjon | Status | Outlook-integrering | Merknader |
|---------|--------|--------------------| --------- |
| **macOS Sonoma (14.x)** | ✅ Støttet | Via Outlook for Mac | Siste versjon |
| **macOS Ventura (13.x)** | ✅ Støttet | Via Outlook for Mac | Støttet |
| **macOS Monterey (12.x)** | ⚠️ Begrenset | Via Outlook for Mac | Mindre kompatibilitetsproblemer |
| **macOS Big Sur (11.x)** | ❌ Ikke støttet | - | For gammel |

#### Linux
| Distribusjon | Status | Outlook-alternativ | Merknader |
|-------------|--------|-------------------|---------- |
| **Ubuntu 22.04+** | ⚠️ Begrenset | Web/Thunderbird | EML-filer støttet |
| **Red Hat Enterprise** | ⚠️ Begrenset | Web/Evolution | Bedriftsmiljø |
| **Alle distribusjoner** | ❌ Ingen innebygd støtte | - | Ingen innebygd Outlook |

## Utgivelsesplan

### Utgivelsessyklus

#### Store utgivelser
- **Aprilutgivelse** (Wave 1): Store nye funksjoner
- **Oktoberutgivelse** (Wave 2): Forbedringer og justeringer

#### Mindre utgivelser
- **Månedlig**: Feilrettinger og mindre forbedringer
- **Hotfixer**: Kritiske problemer innen 48 timer

### Bakoverkompatibilitet
| Aspekt | Policy | Tidsramme |
|--------|--------|----------|
| **API-endringer** | 6 måneders varsel | Endringer som bryter kompatibilitet |
| **UI-endringer** | 3 måneders varsel | Store UI-oppdateringer |
| **Konfigurasjon** | Automatisk migrering | Versjonsoppdateringer |

**Se også:** [Redigere e-poster](editing-emails.md) | [Begrensninger](limitations.md)
