# Unterstützte Versionen

Auf dieser Seite finden Sie eine Übersicht aller unterstützten Versionen und Kompatibilitäten für Edit in Outlook.

## Business Central-Versionen

### Aktuelle Unterstützung

#### Business Central SaaS
| BC-Version | Edit in Outlook-Version | Status | Veröffentlichungsdatum | EOL-Datum |
|-----------|-------------------------|--------|----------------------|-----------|
| **BC 27** | 27.0.46066.0+ | ✅ Aktuell | November 2024 | April 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Unterstützt | April 2024 | Oktober 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Unterstützt | Oktober 2023 | April 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Veraltet | April 2023 | Oktober 2024 |

#### Business Central On-Premises
| BC-Version | Edit in Outlook-Version | Status | Hinweise |
|-----------|-------------------------|--------|---------|
| **BC 27** | 27.0.46066.0+ | ✅ Aktuell | Vollständige Funktionalität |
| **BC 26** | 26.0.45889.0+ | ✅ Unterstützt | Vollständige Funktionalität |
| **BC 25** | 25.0.45294.0+ | ✅ Unterstützt | Eingeschränkte neue Funktionen |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Veraltet | Nur Sicherheitsupdates |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Nicht mehr unterstützt |

### Legacy-Versionen (Separate Repositories)
Für ältere Business Central-Versionen sind spezifische Legacy-Versionen verfügbar:

#### BC 16 (2020 Wave 1)
- **Repository**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Letzte Version**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repository**: `qt-bc-outlookedit-legacy-15`
- **Status**: ❌ End of Life
- **Letzte Version**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repository**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life
- **Letzte Version**: 14.0.xxxxx.0

## Microsoft Office-Versionen

### Office 365 / Microsoft 365

#### Outlook Desktop
| Version | Status | Hinweise |
|---------|--------|---------|
| **Outlook 365 Aktuell** | ✅ Vollständig unterstützt | Empfohlene Plattform |
| **Outlook 365 Semi-Annual** | ✅ Unterstützt | Stabile Unternehmensversion |
| **Outlook 2021 LTSC** | ✅ Unterstützt | On-Premises-Unternehmensversion |
| **Outlook 2019** | ⚠️ Eingeschränkte Unterstützung | Grundlegende Funktionalität |
| **Outlook 2016** | ❌ Nicht unterstützt | Zu alt für EML-Verarbeitung |

#### Outlook Web Access (OWA)
| Version | Status | EML-Unterstützung | Hinweise |
|---------|--------|-------------------|---------|
| **OWA Aktuell** | ✅ Unterstützt | Über Download | Browserabhängig |
| **OWA Government** | ✅ Unterstützt | Über Download | Compliance-genehmigt |

#### Outlook Mobile
| Plattform | Status | Funktionalität |
|-----------|--------|---------------|
| **iOS Outlook** | ✅ Unterstützt | Über Dateifreigabe |
| **Android Outlook** | ✅ Unterstützt | Über Dateifreigabe |
| **Windows Mobile** | ❌ Nicht unterstützt | Plattform eingestellt |

### Office On-Premises
| Version | Status | Installation | Hinweise |
|---------|--------|-------------|---------|
| **Office LTSC 2021** | ✅ Unterstützt | MSI/Click-to-Run | Für Unternehmen empfohlen |
| **Office 2019** | ⚠️ Eingeschränkt | MSI/Click-to-Run | Grundlegende EML-Unterstützung |
| **Office 2016** | ❌ Nicht unterstützt | - | EOL erreicht |

## Browser-Kompatibilität

### Empfohlene Browser

#### Windows
| Browser | Version | Status | Leistung |
|---------|---------|--------|---------|
| **Microsoft Edge** | 118+ | ✅ Ausgezeichnet | Beste Leistung |
| **Chrome** | 118+ | ✅ Ausgezeichnet | Sehr gute Leistung |
| **Firefox** | 118+ | ✅ Gut | Gute Leistung |
| **Internet Explorer** | Alle | ❌ Nicht unterstützt | Veraltet |

#### macOS
| Browser | Version | Status | Leistung |
|---------|---------|--------|---------|
| **Safari** | 16+ | ✅ Gut | Native macOS-Integration |
| **Chrome** | 118+ | ✅ Ausgezeichnet | Plattformübergreifende Konsistenz |
| **Firefox** | 118+ | ✅ Gut | Open-Source-Option |
| **Edge** | 118+ | ✅ Ausgezeichnet | Microsoft-Ökosystem |

### Control Add-in-Anforderungen
- **JavaScript**: ES6+-Unterstützung
- **HTML5**: Canvas- und File-API
- **CSS3**: Flexbox- und Grid-Layouts
- **WebAssembly**: Für PDF-Vorschau (optional)

## Plattform-Unterstützung

### Betriebssysteme

#### Windows
| Version | Status | Outlook-Integration | Hinweise |
|---------|--------|---------------------|---------|
| **Windows 11** | ✅ Vollständig unterstützt | Nativ | Empfohlene Plattform |
| **Windows 10 (1909+)** | ✅ Unterstützt | Nativ | Mindestversion |
| **Windows Server 2022** | ✅ Unterstützt | Terminal Server | Unternehmensszenario |
| **Windows Server 2019** | ✅ Unterstützt | Terminal Server | Legacy-Unternehmen |
| **Windows 8.1** | ❌ Nicht unterstützt | - | EOL erreicht |

#### macOS
| Version | Status | Outlook-Integration | Hinweise |
|---------|--------|---------------------|---------|
| **macOS Sonoma (14.x)** | ✅ Unterstützt | Über Outlook für Mac | Neueste Version |
| **macOS Ventura (13.x)** | ✅ Unterstützt | Über Outlook für Mac | Unterstützt |
| **macOS Monterey (12.x)** | ⚠️ Eingeschränkt | Über Outlook für Mac | Geringfügige Kompatibilitätsprobleme |
| **macOS Big Sur (11.x)** | ❌ Nicht unterstützt | - | Zu alt |

#### Linux
| Distribution | Status | Outlook-Alternative | Hinweise |
|-------------|--------|---------------------|---------|
| **Ubuntu 22.04+** | ⚠️ Eingeschränkt | Web/Thunderbird | EML-Dateien unterstützt |
| **Red Hat Enterprise** | ⚠️ Eingeschränkt | Web/Evolution | Unternehmensumgebung |
| **Alle Distributionen** | ❌ Keine native Unterstützung | - | Kein natives Outlook |

## Veröffentlichungsplan

### Veröffentlichungszyklus

#### Hauptversionen
- **April-Release** (Wave 1): Neue Hauptfunktionen
- **Oktober-Release** (Wave 2): Verbesserungen und Verfeinerungen

#### Nebenversionen
- **Monatlich**: Fehlerbehebungen und kleinere Verbesserungen
- **Hotfixes**: Kritische Probleme innerhalb von 48 Stunden

### Abwärtskompatibilität
| Aspekt | Richtlinie | Zeitrahmen |
|--------|-----------|-----------|
| **API-Änderungen** | 6 Monate Ankündigung | Grundlegende Änderungen |
| **UI-Änderungen** | 3 Monate Ankündigung | Größere UI-Updates |
| **Konfiguration** | Automatische Migration | Versionsaktualisierungen |

**Siehe auch:** [E-Mails bearbeiten](editing-emails.md) | [Einschränkungen](limitations.md)
