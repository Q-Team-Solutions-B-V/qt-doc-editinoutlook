# Ondersteunde versies

Op deze pagina vindt u een overzicht van alle ondersteunde versies en compatibiliteit voor Edit in Outlook.

## Business Central-versies

### Huidige ondersteuning

#### Business Central SaaS
| BC-versie | Edit in Outlook-versie | Status | Releasedatum | EOL-datum |
|-----------|------------------------|--------|--------------|-----------|
| **BC 27** | 27.0.46066.0+ | ✅ Huidig | November 2024 | April 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Ondersteund | April 2024 | Oktober 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Ondersteund | Oktober 2023 | April 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Verouderd | April 2023 | Oktober 2024 |

#### Business Central On-Premises
| BC-versie | Edit in Outlook-versie | Status | Opmerkingen |
|-----------|------------------------|--------|-------------|
| **BC 27** | 27.0.46066.0+ | ✅ Huidig | Volledige functionaliteit |
| **BC 26** | 26.0.45889.0+ | ✅ Ondersteund | Volledige functionaliteit |
| **BC 25** | 25.0.45294.0+ | ✅ Ondersteund | Beperkte nieuwe functies |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Verouderd | Alleen beveiligingsupdates |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Niet langer ondersteund |

### Verouderde versies (aparte opslagplaatsen)
Voor oudere Business Central-versies zijn specifieke verouderde versies beschikbaar:

#### BC 16 (2020 Wave 1)
- **Opslagplaats**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Laatste versie**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Opslagplaats**: `qt-bc-outlookedit-legacy-15`
- **Status**: ❌ End of Life
- **Laatste versie**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Opslagplaats**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life
- **Laatste versie**: 14.0.xxxxx.0

## Microsoft Office-versies

### Office 365 / Microsoft 365

#### Outlook Desktop
| Versie | Status | Opmerkingen |
|--------|--------|-------------|
| **Outlook 365 Huidig** | ✅ Volledig ondersteund | Aanbevolen platform |
| **Outlook 365 Semi-Annual** | ✅ Ondersteund | Stabiele bedrijfsversie |
| **Outlook 2021 LTSC** | ✅ Ondersteund | On-premises bedrijfsversie |
| **Outlook 2019** | ⚠️ Beperkte ondersteuning | Basisfunctionaliteit |
| **Outlook 2016** | ❌ Niet ondersteund | Te oud voor EML-verwerking |

#### Outlook Web Access (OWA)
| Versie | Status | EML-ondersteuning | Opmerkingen |
|--------|--------|-------------------|-------------|
| **OWA Huidig** | ✅ Ondersteund | Via download | Afhankelijk van browser |
| **OWA Government** | ✅ Ondersteund | Via download | Compliancegoedgekeurd |

#### Outlook Mobile
| Platform | Status | Functionaliteit |
|----------|--------|----------------|
| **iOS Outlook** | ✅ Ondersteund | Via bestanden delen |
| **Android Outlook** | ✅ Ondersteund | Via bestanden delen |
| **Windows Mobile** | ❌ Niet ondersteund | Platform stopgezet |

### Office On-Premises
| Versie | Status | Installatie | Opmerkingen |
|--------|--------|-------------|-------------|
| **Office LTSC 2021** | ✅ Ondersteund | MSI/Click-to-Run | Aanbevolen voor bedrijven |
| **Office 2019** | ⚠️ Beperkt | MSI/Click-to-Run | Basis-EML-ondersteuning |
| **Office 2016** | ❌ Niet ondersteund | - | EOL bereikt |

## Browsercompatibiliteit

### Aanbevolen browsers

#### Windows
| Browser | Versie | Status | Prestaties |
|---------|--------|--------|-----------|
| **Microsoft Edge** | 118+ | ✅ Uitstekend | Beste prestaties |
| **Chrome** | 118+ | ✅ Uitstekend | Zeer goede prestaties |
| **Firefox** | 118+ | ✅ Goed | Goede prestaties |
| **Internet Explorer** | Alle | ❌ Niet ondersteund | Afgeschaft |

#### macOS
| Browser | Versie | Status | Prestaties |
|---------|--------|--------|-----------|
| **Safari** | 16+ | ✅ Goed | Native macOS-integratie |
| **Chrome** | 118+ | ✅ Uitstekend | Platformoverschrijdende consistentie |
| **Firefox** | 118+ | ✅ Goed | Open-sourceoptie |
| **Edge** | 118+ | ✅ Uitstekend | Microsoft-ecosysteem |

### Vereisten voor Control-invoegtoepassing
- **JavaScript**: ES6+-ondersteuning
- **HTML5**: Canvas- en File-API
- **CSS3**: Flexbox- en Grid-lay-outs
- **WebAssembly**: Voor PDF-voorbeeld (optioneel)

## Platformondersteuning

### Besturingssystemen

#### Windows
| Versie | Status | Outlook-integratie | Opmerkingen |
|--------|--------|-------------------|-------------|
| **Windows 11** | ✅ Volledig ondersteund | Systeemeigen | Aanbevolen platform |
| **Windows 10 (1909+)** | ✅ Ondersteund | Systeemeigen | Minimumversie |
| **Windows Server 2022** | ✅ Ondersteund | Terminal Server | Bedrijfsscenario |
| **Windows Server 2019** | ✅ Ondersteund | Terminal Server | Verouderd bedrijf |
| **Windows 8.1** | ❌ Niet ondersteund | - | EOL bereikt |

#### macOS
| Versie | Status | Outlook-integratie | Opmerkingen |
|--------|--------|-------------------|-------------|
| **macOS Sonoma (14.x)** | ✅ Ondersteund | Via Outlook voor Mac | Nieuwste versie |
| **macOS Ventura (13.x)** | ✅ Ondersteund | Via Outlook voor Mac | Ondersteund |
| **macOS Monterey (12.x)** | ⚠️ Beperkt | Via Outlook voor Mac | Kleine compatibiliteitsproblemen |
| **macOS Big Sur (11.x)** | ❌ Niet ondersteund | - | Te oud |

#### Linux
| Distributie | Status | Outlook-alternatief | Opmerkingen |
|-------------|--------|--------------------|-----------  |
| **Ubuntu 22.04+** | ⚠️ Beperkt | Web/Thunderbird | EML-bestanden ondersteund |
| **Red Hat Enterprise** | ⚠️ Beperkt | Web/Evolution | Bedrijfsomgeving |
| **Alle distributies** | ❌ Geen systeemeigen ondersteuning | - | Geen systeemeigen Outlook |

## Releaseschema

### Releasecyclus

#### Grote releases
- **Aprilrelease** (Wave 1): Grote nieuwe functies
- **Oktoberrelease** (Wave 2): Verbeteringen en verfijningen

#### Kleine releases
- **Maandelijks**: Bugfixes en kleine verbeteringen
- **Hotfixes**: Kritieke problemen binnen 48 uur

### Achterwaartse compatibiliteit
| Aspect | Beleid | Tijdsframe |
|--------|--------|-----------|
| **API-wijzigingen** | 6 maanden kennisgeving | Incompatibele wijzigingen |
| **UI-wijzigingen** | 3 maanden kennisgeving | Grote UI-updates |
| **Configuratie** | Automatische migratie | Versie-updates |

**Zie ook:** [E-mails bewerken](editing-emails.md) | [Beperkingen](limitations.md)
