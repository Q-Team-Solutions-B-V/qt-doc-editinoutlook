# Begrænsninger

Denne side beskriver de kendte begrænsninger, restriktioner og overvejelser ved brug af Edit in Outlook.

## Tekniske begrænsninger

### Browser- og downloadbegrænsninger

#### Filstørrelsesbegrænsninger
| Komponent | Maksimal størrelse | Årsag | Løsning |
|-----------|-------------------|-------|---------|
| **EML-fil** | 25 MB | Browser-downloadgrænse | Opdel store vedhæftninger |
| **PDF-vedhæftninger** | 20 MB | E-mailklientgrænser | Komprimer PDF |
| **Samlet e-mail** | 30 MB | Outlook/Exchange-grænse | Brug SharePoint-links |
| **Control Add-in** | 100 MB hukommelse | Browserpræstation | Opdater siden |

#### Browserspesifikke problemer
- **Chrome**: Pop-up-blokkering kan blokere downloads
- **Firefox**: Kodningsproblemer med ikke-ASCII-tegn
- **Edge**: Lejlighedsvis timeout med store filer
- **Safari**: Begrænset understøttelse af PDF-forhåndsvisning

### Business Central-platformbegrænsninger

#### SaaS vs. On-Premise
| Funktionalitet | SaaS | On-Premise | Bemærk |
|----------------|------|------------|-------|
| **Automatiske opdateringer** | ✅ | ❌ | SaaS automatisk, On-Premise manuelt |
| **Brugerdefinerede udvidelser** | ⚠️ Begrænset | ✅ Fuld | SaaS-sandboxbegrænsninger |
| **Fejlfindingstilstand** | ❌ | ✅ | SaaS-sikkerhedspolitik |
| **Logadgang** | ⚠️ Application Insights | ✅ Direkte | Forskellige logningsmetoder |

#### API-grænser
- **Anmodninger pr. minut**: 100 (SaaS), Ubegrænset (On-Premise)
- **Sessionstimeout**: 30 minutter som standard
- **Samtidige brugere**: Baseret på licensmodel

## Outlook- og Office-begrænsninger

### Outlook Desktop vs. Web

#### Funktionssammenligning
| Funktion | Desktop | Web | Mobil |
|----------|---------|-----|-------|
| **EML-åbning** | ✅ Nativ | ⚠️ Via browser | ❌ Begrænset |
| **Udvidet formatering** | ✅ Fuld | ✅ Fuld | ⚠️ Grundlæggende |
| **Vedhæftningshåndtering** | ✅ Fuld | ✅ Fuld | ⚠️ Kun upload |
| **Offlineadgang** | ✅ Fuld | ❌ Ingen | ⚠️ Begrænset |

#### Versionsafhængigheder
- **Outlook 2016/2019**: Begrænset EML-understøttelse
- **OWA Legacy**: Ingen direkte EML-åbning
- **Mobilapps**: Kræver forberedelsestrin på skrivebordet

### Exchange- og O365-grænser

#### E-mailstørrelsesgrænser
| Platform | Maks. beskedstørrelse | Maks. vedhæftninger | Maks. modtagere |
|----------|-----------------------|---------------------|----------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (standard) | Ubegrænset | 5000 |
| **Exchange 2016** | 25 MB (standard) | Ubegrænset | 5000 |

> **Bemærk**: Organisationsindstillinger kan yderligere begrænse disse grænser

## Dokumenttypebegrænsninger

### Understøttet vs. ikke understøttet

#### Fuldt understøttet
- ✅ Salgstilbud, -ordrer, -fakturaer
- ✅ Indkøbsordrer, -fakturaer
- ✅ Bogførte dokumenter
- ✅ Kreditnotaer
- ✅ Lagerleverancer

#### Begrænset understøttelse
- ⚠️ **Servicedokumenter**: Grundlæggende skabelonunderstøttelse
- ⚠️ **Projektdokumenter**: Minimal personalisering
- ⚠️ **Montageordrer**: Ingen specifikke skabeloner

#### Ikke understøttet
- ❌ **Brugerdefinerede rapportobjekter**: Ingen EML-generering
- ❌ **Dataverse-integration**: Kun BC-nativ
- ❌ **Eksterne dokumenter**: Ingen tredjepartsunderstøttelse

### Skabelonbegrænsninger

#### HTML-skabelonproblemer

```html
/* Problematisk CSS */
.ikke-understottet {
    position: absolute;  /* Ikke bredt understøttet */
    transform: rotate(); /* E-mailklientproblemer */
    /* @media queries — Begrænset understøttelse */
}
```

#### Understøttet HTML-delmængde
- ✅ Grundlæggende HTML-tags (p, div, table, br)
- ✅ CSS-formatering (inline foretrækkes)
- ✅ Billeder (indlejret eller linket)
- ❌ JavaScript (sikkerhedsblokeret)
- ❌ Komplekse CSS-layouts (flexbox, grid)
- ❌ Ekstern skriftindlæsning

## Bruger- og rettighedsbegrænsninger

### Tilladelsesafhængigheder

#### Mindste nødvendige rettigheder
En bruger skal som minimum have:
- **Dokumentlæsning**: Til dokumentadgang
- **E-mailskabelonlæsning**: Til skabelonadgang
- **Fildownload**: Til EML-filer
- **Control Add-in-udførelse**: Til browserfunktionalitet

**Se også:** [Redigering af e-mails](editing-emails.md) | [Understøttede versioner](supported-versions.md)
