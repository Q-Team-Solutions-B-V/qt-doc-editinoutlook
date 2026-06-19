# Ograniczenia

Ta strona opisuje znane ograniczenia, restrykcje i kwestie do rozważenia podczas korzystania z Edit in Outlook.

## Ograniczenia techniczne

### Ograniczenia przeglądarki i pobierania

#### Limity rozmiaru pliku
| Składnik | Maksymalny rozmiar | Przyczyna | Obejście |
|----------|-------------------|-----------|----------|
| **Plik EML** | 25 MB | Limit pobierania przeglądarki | Podziel duże załączniki |
| **Załączniki PDF** | 20 MB | Limity klienta poczty e-mail | Skompresuj PDF |
| **Cała wiadomość e-mail** | 30 MB | Limit Outlook/Exchange | Użyj łączy SharePoint |
| **Control Add-in** | 100 MB pamięci | Wydajność przeglądarki | Odśwież stronę |

#### Problemy specyficzne dla przeglądarek
- **Chrome**: Blokowanie wyskakujących okien może blokować pobieranie
- **Firefox**: Problemy z kodowaniem znaków innych niż ASCII
- **Edge**: Sporadyczny limit czasu przy dużych plikach
- **Safari**: Ograniczona obsługa podglądu PDF

### Ograniczenia platformy Business Central

#### SaaS a instalacja lokalna
| Funkcjonalność | SaaS | Lokalna | Uwaga |
|----------------|------|---------|-------|
| **Automatyczne aktualizacje** | ✅ | ❌ | SaaS automatycznie, instalacja lokalna ręcznie |
| **Rozszerzenia niestandardowe** | ⚠️ Ograniczone | ✅ Pełne | Ograniczenia piaskownicy SaaS |
| **Tryb debugowania** | ❌ | ✅ | Zasady zabezpieczeń SaaS |
| **Dostęp do dzienników** | ⚠️ Application Insights | ✅ Bezpośredni | Różne podejścia do rejestrowania |

#### Limity interfejsu API
- **Żądania na minutę**: 100 (SaaS), Bez ograniczeń (lokalna)
- **Limit czasu sesji**: domyślnie 30 minut
- **Jednoczesni użytkownicy**: Na podstawie modelu licencji

## Ograniczenia programów Outlook i Office

### Outlook Desktop a wersja internetowa

#### Porównanie funkcji
| Funkcja | Desktop | Internet | Urządzenia mobilne |
|---------|---------|----------|--------------------|
| **Otwieranie EML** | ✅ Natywne | ⚠️ Przez przeglądarkę | ❌ Ograniczone |
| **Zaawansowane formatowanie** | ✅ Pełne | ✅ Pełne | ⚠️ Podstawowe |
| **Obsługa załączników** | ✅ Pełna | ✅ Pełna | ⚠️ Tylko przesyłanie |
| **Dostęp offline** | ✅ Pełny | ❌ Brak | ⚠️ Ograniczony |

#### Zależności wersji
- **Outlook 2016/2019**: Ograniczona obsługa EML
- **OWA Legacy**: Brak bezpośredniego otwierania EML
- **Aplikacje mobilne**: Wymagany krok przygotowawczy na komputerze

### Limity Exchange i O365

#### Limity rozmiaru wiadomości e-mail
| Platforma | Maks. rozmiar wiadomości | Maks. załączniki | Maks. odbiorcy |
|-----------|------------------------|-----------------|----------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (domyślnie) | Bez ograniczeń | 5000 |
| **Exchange 2016** | 25 MB (domyślnie) | Bez ograniczeń | 5000 |

> **Uwaga**: Ustawienia organizacji mogą dodatkowo ograniczać te limity

## Ograniczenia typów dokumentów

### Obsługiwane a nieobsługiwane

#### W pełni obsługiwane
- ✅ Oferty, zamówienia, faktury sprzedaży
- ✅ Zamówienia, faktury zakupu
- ✅ Zaksięgowane dokumenty
- ✅ Faktury korygujące
- ✅ Wydania magazynowe

#### Ograniczona obsługa
- ⚠️ **Dokumenty serwisowe**: Podstawowa obsługa szablonów
- ⚠️ **Dokumenty projektowe**: Minimalna personalizacja
- ⚠️ **Zlecenia montażu**: Brak określonych szablonów

#### Nieobsługiwane
- ❌ **Niestandardowe obiekty raportów**: Brak generowania EML
- ❌ **Integracja Dataverse**: Tylko natywne BC
- ❌ **Dokumenty zewnętrzne**: Brak obsługi innych firm

### Ograniczenia szablonów

#### Problemy z szablonami HTML

```html
/* Problematyczny CSS */
.nieobslugiwane {
    position: absolute;  /* Nie jest powszechnie obsługiwane */
    transform: rotate(); /* Problemy z klientami poczty e-mail */
    /* @media queries — Ograniczona obsługa */
}
```

#### Obsługiwany podzbiór HTML
- ✅ Podstawowe tagi HTML (p, div, table, br)
- ✅ Style CSS (preferowane wbudowane)
- ✅ Obrazy (osadzone lub połączone)
- ❌ JavaScript (zablokowane ze względów bezpieczeństwa)
- ❌ Złożone układy CSS (flexbox, grid)
- ❌ Ładowanie zewnętrznych czcionek

## Ograniczenia użytkownika i uprawnień

### Zależności uprawnień

#### Minimalne wymagane uprawnienia
Użytkownik potrzebuje co najmniej:
- **Odczyt dokumentów**: Dostęp do dokumentów
- **Odczyt szablonu wiadomości e-mail**: Dostęp do szablonów
- **Pobieranie pliku**: Pliki EML
- **Wykonywanie Control Add-in**: Funkcjonalność przeglądarki

**Zobacz też:** [Edytowanie wiadomości e-mail](editing-emails.md) | [Obsługiwane wersje](supported-versions.md)
