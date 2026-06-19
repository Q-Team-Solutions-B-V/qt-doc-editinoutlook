# Understøttede versioner

Denne side giver et overblik over alle understøttede versioner og kompatibilitet for Edit in Outlook.

## Business Central-versioner

### Aktuel understøttelse

#### Business Central SaaS
| BC-version | Edit in Outlook-version | Status | Udgivelsesdato | EOL-dato |
|-----------|------------------------|--------|---------------|---------|
| **BC 27** | 27.0.46066.0+ | ✅ Aktuel | November 2024 | April 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Understøttet | April 2024 | Oktober 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Understøttet | Oktober 2023 | April 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Ældre | April 2023 | Oktober 2024 |

#### Business Central On-Premise
| BC-version | Edit in Outlook-version | Status | Bemærkninger |
|-----------|------------------------|--------|-------------|
| **BC 27** | 27.0.46066.0+ | ✅ Aktuel | Fuld funktionalitet |
| **BC 26** | 26.0.45889.0+ | ✅ Understøttet | Fuld funktionalitet |
| **BC 25** | 25.0.45294.0+ | ✅ Understøttet | Begrænsede nye funktioner |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Ældre | Kun sikkerhedsopdateringer |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Ikke længere understøttet |

### Ældre versioner (Separate repositories)
For ældre Business Central-versioner er specifikke ældre versioner tilgængelige:

#### BC 16 (2020 Wave 1)
- **Repository**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Seneste version**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repository**: `qt-bc-outlookedit-legacy-15`
- **Status**: ❌ End of Life
- **Seneste version**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repository**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life
- **Seneste version**: 14.0.xxxxx.0

## Microsoft Office-versioner

### Office 365 / Microsoft 365

#### Outlook Desktop
| Version | Status | Bemærkninger |
|---------|--------|-------------|
| **Outlook 365 Aktuel** | ✅ Fuldt understøttet | Anbefalet platform |
| **Outlook 365 Semi-Annual** | ✅ Understøttet | Stabil virksomhedsversion |
| **Outlook 2021 LTSC** | ✅ Understøttet | On-premise virksomhed |
| **Outlook 2019** | ⚠️ Begrænset understøttelse | Grundlæggende funktionalitet |
| **Outlook 2016** | ❌ Ikke understøttet | For gammel til EML |

#### Outlook Web Access (OWA)
| Version | Status | EML-understøttelse | Bemærkninger |
|---------|--------|-------------------|-------------|
| **OWA Aktuel** | ✅ Understøttet | Via download | Browserafhængig |
| **OWA Government** | ✅ Understøttet | Via download | Overholdelsegodkendt |

#### Outlook Mobile
| Platform | Status | Funktionalitet |
|----------|--------|---------------|
| **iOS Outlook** | ✅ Understøttet | Via fildeling |
| **Android Outlook** | ✅ Understøttet | Via fildeling |
| **Windows Mobile** | ❌ Ikke understøttet | Platform udgået |

### Office On-Premise
| Version | Status | Installation | Bemærkninger |
|---------|--------|-------------|-------------|
| **Office LTSC 2021** | ✅ Understøttet | MSI/Click-to-Run | Anbefalet til virksomheder |
| **Office 2019** | ⚠️ Begrænset | MSI/Click-to-Run | Grundlæggende EML-understøttelse |
| **Office 2016** | ❌ Ikke understøttet | - | EOL nået |

## Browserkompatibilitet

### Anbefalede browsere

#### Windows
| Browser | Version | Status | Ydeevne |
|---------|---------|--------|---------|
| **Microsoft Edge** | 118+ | ✅ Fremragende | Bedste ydeevne |
| **Chrome** | 118+ | ✅ Fremragende | Meget god ydeevne |
| **Firefox** | 118+ | ✅ God | God ydeevne |
| **Internet Explorer** | Alle | ❌ Ikke understøttet | Forældet |

#### macOS
| Browser | Version | Status | Ydeevne |
|---------|---------|--------|---------|
| **Safari** | 16+ | ✅ God | Nativ macOS-integration |
| **Chrome** | 118+ | ✅ Fremragende | Tværplatformskonsistens |
| **Firefox** | 118+ | ✅ God | Open source-mulighed |
| **Edge** | 118+ | ✅ Fremragende | Microsoft-økosystem |

### Control Add-in-krav
- **JavaScript**: ES6+-understøttelse
- **HTML5**: Canvas og File API
- **CSS3**: Flexbox- og Grid-layouts
- **WebAssembly**: Til PDF-forhåndsvisning (valgfrit)

## Platformunderstøttelse

### Operativsystemer

#### Windows
| Version | Status | Outlook-integration | Bemærkninger |
|---------|--------|--------------------|-----------   |
| **Windows 11** | ✅ Fuldt understøttet | Nativ | Anbefalet platform |
| **Windows 10 (1909+)** | ✅ Understøttet | Nativ | Minimumversion |
| **Windows Server 2022** | ✅ Understøttet | Terminal Server | Virksomhedsscenarie |
| **Windows Server 2019** | ✅ Understøttet | Terminal Server | Ældre virksomhed |
| **Windows 8.1** | ❌ Ikke understøttet | - | EOL nået |

#### macOS
| Version | Status | Outlook-integration | Bemærkninger |
|---------|--------|--------------------|-----------   |
| **macOS Sonoma (14.x)** | ✅ Understøttet | Via Outlook til Mac | Seneste version |
| **macOS Ventura (13.x)** | ✅ Understøttet | Via Outlook til Mac | Understøttet |
| **macOS Monterey (12.x)** | ⚠️ Begrænset | Via Outlook til Mac | Mindre kompatibilitetsproblemer |
| **macOS Big Sur (11.x)** | ❌ Ikke understøttet | - | For gammel |

#### Linux
| Distribution | Status | Outlook-alternativ | Bemærkninger |
|-------------|--------|-------------------|------------- |
| **Ubuntu 22.04+** | ⚠️ Begrænset | Web/Thunderbird | EML-filer understøttet |
| **Red Hat Enterprise** | ⚠️ Begrænset | Web/Evolution | Virksomhedsmiljø |
| **Alle distributioner** | ❌ Ingen nativ understøttelse | - | Ingen nativ Outlook |

## Udgivelsesplan

### Udgivelsescyklus

#### Større udgivelser
- **Apriludgivelse** (Wave 1): Nye større funktioner
- **Oktoberudgivelse** (Wave 2): Forbedringer og justeringer

#### Mindre udgivelser
- **Månedligt**: Fejlrettelser og mindre forbedringer
- **Hotfixes**: Kritiske problemer inden for 48 timer

### Bagudkompatibilitet
| Aspekt | Politik | Tidsramme |
|--------|---------|----------|
| **API-ændringer** | 6 måneders varsel | Ændringer der bryder kompatibilitet |
| **UI-ændringer** | 3 måneders varsel | Større UI-opdateringer |
| **Konfiguration** | Automatisk migrering | Versionsopdateringer |

**Se også:** [Redigering af e-mails](editing-emails.md) | [Begrænsninger](limitations.md)
