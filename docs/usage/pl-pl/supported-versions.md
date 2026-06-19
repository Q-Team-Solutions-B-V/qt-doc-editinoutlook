# Obsługiwane wersje

Ta strona zawiera przegląd wszystkich obsługiwanych wersji i zgodności dla Edit in Outlook.

## Wersje Business Central

### Bieżące wsparcie

#### Business Central SaaS
| Wersja BC | Wersja Edit in Outlook | Status | Data wydania | Data EOL |
|-----------|------------------------|--------|--------------|---------|
| **BC 27** | 27.0.46066.0+ | ✅ Bieżąca | Listopad 2024 | Kwiecień 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Obsługiwana | Kwiecień 2024 | Październik 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Obsługiwana | Październik 2023 | Kwiecień 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Starszy | Kwiecień 2023 | Październik 2024 |

#### Business Central — instalacja lokalna
| Wersja BC | Wersja Edit in Outlook | Status | Uwagi |
|-----------|------------------------|--------|-------|
| **BC 27** | 27.0.46066.0+ | ✅ Bieżąca | Pełna funkcjonalność |
| **BC 26** | 26.0.45889.0+ | ✅ Obsługiwana | Pełna funkcjonalność |
| **BC 25** | 25.0.45294.0+ | ✅ Obsługiwana | Ograniczone nowe funkcje |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Starszy | Tylko aktualizacje zabezpieczeń |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Nie jest już obsługiwana |

### Starsze wersje (osobne repozytoria)
Dla starszych wersji Business Central dostępne są określone starsze wersje:

#### BC 16 (2020 Wave 1)
- **Repozytorium**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Ostatnia wersja**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repozytorium**: `qt-bc-outlookedit-legacy-15`
- **Status**: ❌ End of Life
- **Ostatnia wersja**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repozytorium**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life
- **Ostatnia wersja**: 14.0.xxxxx.0

## Wersje Microsoft Office

### Office 365 / Microsoft 365

#### Outlook Desktop
| Wersja | Status | Uwagi |
|--------|--------|-------|
| **Outlook 365 Bieżąca** | ✅ W pełni obsługiwana | Zalecana platforma |
| **Outlook 365 Semi-Annual** | ✅ Obsługiwana | Stabilna wersja dla przedsiębiorstw |
| **Outlook 2021 LTSC** | ✅ Obsługiwana | Instalacja lokalna dla przedsiębiorstw |
| **Outlook 2019** | ⚠️ Ograniczone wsparcie | Podstawowa funkcjonalność |
| **Outlook 2016** | ❌ Nieobsługiwana | Zbyt stara dla obsługi EML |

#### Outlook Web Access (OWA)
| Wersja | Status | Obsługa EML | Uwagi |
|--------|--------|------------|-------|
| **OWA Bieżąca** | ✅ Obsługiwana | Przez pobieranie | Zależna od przeglądarki |
| **OWA Government** | ✅ Obsługiwana | Przez pobieranie | Zatwierdzona pod kątem zgodności |

#### Outlook Mobile
| Platforma | Status | Funkcjonalność |
|-----------|--------|----------------|
| **iOS Outlook** | ✅ Obsługiwana | Przez udostępnianie plików |
| **Android Outlook** | ✅ Obsługiwana | Przez udostępnianie plików |
| **Windows Mobile** | ❌ Nieobsługiwana | Platforma wycofana |

### Office — instalacja lokalna
| Wersja | Status | Instalacja | Uwagi |
|--------|--------|-----------|-------|
| **Office LTSC 2021** | ✅ Obsługiwana | MSI/Click-to-Run | Zalecana dla przedsiębiorstw |
| **Office 2019** | ⚠️ Ograniczone | MSI/Click-to-Run | Podstawowa obsługa EML |
| **Office 2016** | ❌ Nieobsługiwana | - | EOL osiągnięte |

## Zgodność przeglądarek

### Zalecane przeglądarki

#### Windows
| Przeglądarka | Wersja | Status | Wydajność |
|-------------|--------|--------|----------|
| **Microsoft Edge** | 118+ | ✅ Doskonała | Najlepsza wydajność |
| **Chrome** | 118+ | ✅ Doskonała | Bardzo dobra wydajność |
| **Firefox** | 118+ | ✅ Dobra | Dobra wydajność |
| **Internet Explorer** | Wszystkie | ❌ Nieobsługiwana | Przestarzała |

#### macOS
| Przeglądarka | Wersja | Status | Wydajność |
|-------------|--------|--------|----------|
| **Safari** | 16+ | ✅ Dobra | Natywna integracja z macOS |
| **Chrome** | 118+ | ✅ Doskonała | Spójność na różnych platformach |
| **Firefox** | 118+ | ✅ Dobra | Opcja open source |
| **Edge** | 118+ | ✅ Doskonała | Ekosystem Microsoft |

### Wymagania Control Add-in
- **JavaScript**: Obsługa ES6+
- **HTML5**: Canvas i File API
- **CSS3**: Układy Flexbox i Grid
- **WebAssembly**: Do podglądu PDF (opcjonalnie)

## Obsługa platformy

### Systemy operacyjne

#### Windows
| Wersja | Status | Integracja z programem Outlook | Uwagi |
|--------|--------|-------------------------------|-------|
| **Windows 11** | ✅ W pełni obsługiwany | Natywna | Zalecana platforma |
| **Windows 10 (1909+)** | ✅ Obsługiwany | Natywna | Minimalna wersja |
| **Windows Server 2022** | ✅ Obsługiwany | Terminal Server | Scenariusz dla przedsiębiorstw |
| **Windows Server 2019** | ✅ Obsługiwany | Terminal Server | Starsza wersja dla przedsiębiorstw |
| **Windows 8.1** | ❌ Nieobsługiwany | - | EOL osiągnięte |

#### macOS
| Wersja | Status | Integracja z programem Outlook | Uwagi |
|--------|--------|-------------------------------|-------|
| **macOS Sonoma (14.x)** | ✅ Obsługiwany | Przez program Outlook dla komputerów Mac | Najnowsza wersja |
| **macOS Ventura (13.x)** | ✅ Obsługiwany | Przez program Outlook dla komputerów Mac | Obsługiwany |
| **macOS Monterey (12.x)** | ⚠️ Ograniczone | Przez program Outlook dla komputerów Mac | Niewielkie problemy ze zgodnością |
| **macOS Big Sur (11.x)** | ❌ Nieobsługiwany | - | Zbyt stary |

#### Linux
| Dystrybucja | Status | Alternatywa dla programu Outlook | Uwagi |
|-------------|--------|----------------------------------|-------|
| **Ubuntu 22.04+** | ⚠️ Ograniczone | Web/Thunderbird | Pliki EML obsługiwane |
| **Red Hat Enterprise** | ⚠️ Ograniczone | Web/Evolution | Środowisko przedsiębiorstwa |
| **Wszystkie dystrybucje** | ❌ Brak natywnej obsługi | - | Brak natywnego programu Outlook |

## Harmonogram wydań

### Cykl wydawniczy

#### Główne wydania
- **Wydanie kwietniowe** (Wave 1): Nowe główne funkcje
- **Wydanie październikowe** (Wave 2): Ulepszenia i udoskonalenia

#### Pomniejsze wydania
- **Miesięczne**: Poprawki błędów i drobne ulepszenia
- **Poprawki awaryjne**: Krytyczne problemy w ciągu 48 godzin

### Zgodność wsteczna
| Aspekt | Zasady | Ramy czasowe |
|--------|--------|-------------|
| **Zmiany w interfejsie API** | Powiadomienie z 6-miesięcznym wyprzedzeniem | Zmiany powodujące niezgodność |
| **Zmiany interfejsu użytkownika** | Powiadomienie z 3-miesięcznym wyprzedzeniem | Duże aktualizacje interfejsu |
| **Konfiguracja** | Automatyczna migracja | Aktualizacje wersji |

**Zobacz też:** [Edytowanie wiadomości e-mail](editing-emails.md) | [Ograniczenia](limitations.md)
