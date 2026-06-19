# Begrensninger

Denne siden beskriver de kjente begrensningene, restriksjonene og hensynene ved bruk av Edit in Outlook.

## Tekniske begrensninger

### Nettleser- og nedlastingsbegrensninger

#### Filstørrelsesbegrensninger
| Komponent | Maksimal størrelse | Årsak | Løsning |
|-----------|------------------|-------|---------|
| **EML-fil** | 25 MB | Nettlesernedlastingsgrense | Del opp store vedlegg |
| **PDF-vedlegg** | 20 MB | E-postklientgrenser | Komprimer PDF |
| **Total e-post** | 30 MB | Outlook/Exchange-grense | Bruk SharePoint-lenker |
| **Control Add-in** | 100 MB minne | Nettleserytelse | Oppdater siden |

#### Nettleserspesifikke problemer
- **Chrome**: Pop-up-blokkering kan blokkere nedlastinger
- **Firefox**: Kodingsproblemer med ikke-ASCII-tegn
- **Edge**: Sporadisk tidsavbrudd med store filer
- **Safari**: Begrenset støtte for PDF-forhåndsvisning

### Business Central-plattformbegrensninger

#### SaaS vs. On-Premise
| Funksjonalitet | SaaS | On-Premise | Merk |
|----------------|------|------------|------|
| **Automatiske oppdateringer** | ✅ | ❌ | SaaS automatisk, On-Premise manuelt |
| **Egendefinerte utvidelser** | ⚠️ Begrenset | ✅ Full | SaaS-sandkasserestriksjoner |
| **Feilsøkingsmodus** | ❌ | ✅ | SaaS-sikkerhetspolicy |
| **Loggtilgang** | ⚠️ Application Insights | ✅ Direkte | Ulike loggingsmetoder |

#### API-grenser
- **Forespørsler per minutt**: 100 (SaaS), Ubegrenset (On-Premise)
- **Tidsavbrudd for økt**: 30 minutter som standard
- **Samtidige brukere**: Basert på lisensmodell

## Outlook- og Office-begrensninger

### Outlook Desktop vs. Web

#### Funksjonsammenligning
| Funksjon | Desktop | Web | Mobil |
|----------|---------|-----|-------|
| **EML-åpning** | ✅ Innebygd | ⚠️ Via nettleser | ❌ Begrenset |
| **Utvidet formatering** | ✅ Full | ✅ Full | ⚠️ Grunnleggende |
| **Vedleggsbehandling** | ✅ Full | ✅ Full | ⚠️ Bare opplasting |
| **Frakoblet tilgang** | ✅ Full | ❌ Ingen | ⚠️ Begrenset |

#### Versjonsavhengigheter
- **Outlook 2016/2019**: Begrenset EML-støtte
- **OWA Legacy**: Ingen direkte EML-åpning
- **Mobilapper**: Krever forberedende trinn på skrivebordet

### Exchange- og O365-grenser

#### E-poststørrelsesgrenser
| Plattform | Maks. meldingsstørrelse | Maks. vedlegg | Maks. mottakere |
|-----------|------------------------|--------------|----------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (standard) | Ubegrenset | 5000 |
| **Exchange 2016** | 25 MB (standard) | Ubegrenset | 5000 |

> **Merk**: Organisasjonsinnstillinger kan ytterligere begrense disse grensene

## Dokumenttypebegrensninger

### Støttet vs. ikke støttet

#### Fullt støttet
- ✅ Salgstilbud, -ordrer, -fakturaer
- ✅ Innkjøpsordrer, -fakturaer
- ✅ Bokførte dokumenter
- ✅ Kreditnotaer
- ✅ Lagerforsendelser

#### Begrenset støtte
- ⚠️ **Servicedokumenter**: Grunnleggende malstøtte
- ⚠️ **Prosjektdokumenter**: Minimal personalisering
- ⚠️ **Monteringsordrer**: Ingen spesifikke maler

#### Ikke støttet
- ❌ **Egendefinerte rapportobjekter**: Ingen EML-generering
- ❌ **Dataverse-integrering**: Bare BC-nativ
- ❌ **Eksterne dokumenter**: Ingen tredjepartsstøtte

### Malbegrensninger

#### HTML-malproblemer

```html
/* Problematisk CSS */
.ikke-stoettet {
    position: absolute;  /* Ikke bredt støttet */
    transform: rotate(); /* E-postklientproblemer */
    /* @media queries — Begrenset støtte */
}
```

#### Støttet HTML-delsett
- ✅ Grunnleggende HTML-koder (p, div, table, br)
- ✅ CSS-formatering (innebygd foretrekkes)
- ✅ Bilder (innebygd eller koblet)
- ❌ JavaScript (sikkerhetsblokert)
- ❌ Komplekse CSS-oppsett (flexbox, grid)
- ❌ Ekstern skriftlasting

## Bruker- og rettighetsbegrensninger

### Tillatelsesavhengigheter

#### Minimum nødvendige rettigheter
En bruker trenger minimum:
- **Dokumentlesing**: For dokumenttilgang
- **E-postmallesing**: For maltilgang
- **Filnedlasting**: For EML-filer
- **Control Add-in-kjøring**: For nettleserfunksjonalitet

**Se også:** [Redigere e-poster](editing-emails.md) | [Støttede versjoner](supported-versions.md)
