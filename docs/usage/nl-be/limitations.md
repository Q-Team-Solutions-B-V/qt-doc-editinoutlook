# Beperkingen

Op deze pagina worden de bekende beperkingen, restricties en overwegingen beschreven bij het gebruik van Edit in Outlook.

## Technische beperkingen

### Browser- en downloadbeperkingen

#### Bestandsgroottebeperkingen
| Onderdeel | Maximale grootte | Reden | Oplossing |
|-----------|-----------------|-------|-----------|
| **EML-bestand** | 25 MB | Browserlimiet voor downloads | Grote bijlagen splitsen |
| **PDF-bijlagen** | 20 MB | E-mailclientlimieten | PDF comprimeren |
| **Totale e-mail** | 30 MB | Outlook/Exchange-limiet | SharePoint-koppelingen gebruiken |
| **Control-invoegtoepassing** | 100 MB geheugen | Browserprestaties | Pagina vernieuwen |

#### Browsergerelateerde problemen
- **Chrome**: Pop-upblokkering kan downloads blokkeren
- **Firefox**: Coderingsproblemen met niet-ASCII-tekens
- **Edge**: Af en toe time-out bij grote bestanden
- **Safari**: Beperkte ondersteuning voor PDF-voorbeeld

### Business Central-platformbeperkingen

#### SaaS versus On-Premises
| Functionaliteit | SaaS | On-Premises | Opmerking |
|-----------------|------|-------------|-----------|
| **Automatische updates** | ✅ | ❌ | SaaS automatisch, On-Premises handmatig |
| **Aangepaste extensies** | ⚠️ Beperkt | ✅ Volledig | SaaS-sandboxbeperkingen |
| **Foutopsporingsmodus** | ❌ | ✅ | SaaS-beveiligingsbeleid |
| **Logtoegang** | ⚠️ Application Insights | ✅ Direct | Verschillende logbenaderingen |

#### API-limieten
- **Aanvragen per minuut**: 100 (SaaS), Onbeperkt (On-Premises)
- **Sessietime-out**: standaard 30 minuten
- **Gelijktijdige gebruikers**: op basis van licentiemodel

## Outlook- en Office-beperkingen

### Outlook Desktop versus Web

#### Functievergelijking
| Functie | Desktop | Web | Mobiel |
|---------|---------|-----|--------|
| **EML openen** | ✅ Systeemeigen | ⚠️ Via browser | ❌ Beperkt |
| **Uitgebreide opmaak** | ✅ Volledig | ✅ Volledig | ⚠️ Basis |
| **Bijlagebeheer** | ✅ Volledig | ✅ Volledig | ⚠️ Alleen uploaden |
| **Offlinesoegang** | ✅ Volledig | ❌ Geen | ⚠️ Beperkt |

#### Versieafhankelijkheden
- **Outlook 2016/2019**: Beperkte EML-ondersteuning
- **OWA Legacy**: Geen directe EML-opening
- **Mobiele apps**: Vereist voorbereidingsstap op desktop

### Exchange- en O365-limieten

#### E-mailgroottebeperkingen
| Platform | Max. berichtgrootte | Max. bijlagen | Max. ontvangers |
|----------|--------------------|--------------|--------------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (standaard) | Onbeperkt | 5000 |
| **Exchange 2016** | 25 MB (standaard) | Onbeperkt | 5000 |

> **Opmerking**: Organisatie-instellingen kunnen deze limieten verder beperken

## Documenttypebeperkingen

### Ondersteund versus niet-ondersteund

#### Volledig ondersteund
- ✅ Verkoopoffertes, -orders, -facturen
- ✅ Inkooporders, -facturen
- ✅ Geboekte documenten
- ✅ Creditnota's
- ✅ Magazijnverzendingen

#### Beperkte ondersteuning
- ⚠️ **Servicedocumenten**: Basissjabloonondersteuning
- ⚠️ **Projectdocumenten**: Minimale personalisatie
- ⚠️ **Assemblageorders**: Geen specifieke sjablonen

#### Niet ondersteund
- ❌ **Aangepaste rapportobjecten**: Geen EML-generatie
- ❌ **Dataverse-integratie**: Alleen BC-eigen
- ❌ **Externe documenten**: Geen ondersteuning van derden

### Sjabloonbeperkingen

#### HTML-sjabloonproblemen

```html
/* Problematische CSS */
.niet-ondersteund {
    position: absolute;  /* Niet breed ondersteund */
    transform: rotate(); /* E-mailclientproblemen */
    /* @media queries — Beperkte ondersteuning */
}
```

#### Ondersteunde HTML-subset
- ✅ Basis-HTML-tags (p, div, table, br)
- ✅ CSS-opmaak (inline aanbevolen)
- ✅ Afbeeldingen (ingesloten of gekoppeld)
- ❌ JavaScript (beveiligingsbeperking)
- ❌ Complexe CSS-lay-outs (flexbox, grid)
- ❌ Extern lettertype laden

## Gebruikers- en rechtenbeperkingen

### Machtigingsafhankelijkheden

#### Minimaal vereiste rechten
Een gebruiker heeft minimaal nodig:
- **Documenten lezen**: Voor documenttoegang
- **E-mailsjabloon lezen**: Voor sjabloontoegang
- **Bestanden downloaden**: Voor EML-bestanden
- **Control-invoegtoepassing uitvoeren**: Voor browserfunctionaliteit

**Zie ook:** [E-mails bewerken](editing-emails.md) | [Ondersteunde versies](supported-versions.md)
