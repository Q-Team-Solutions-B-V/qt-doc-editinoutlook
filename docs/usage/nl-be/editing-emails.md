# E-mails bewerken

Op deze pagina wordt beschreven hoe u Edit in Outlook gebruikt om e-mails van Business Central-documenten te bewerken en te verzenden via Microsoft Outlook.

## Basiswerkstroom

### Stap-voor-stap-proces

#### 1. Documentkeuze
1. **Open een Business Central-document** (bijv. verkoopofferte, factuur, order)
2. **Klik op "E-mail verzenden"** in het lint
3. **Het e-maildialoogvenster wordt geopend**

#### 2. Edit in Outlook activeren
1. **In het e-maildialoogvenster**:
   - Selecteer ontvangers
   - Kies een e-mailsjabloon (optioneel)
   - **Klik op "Bewerken in Outlook"**
2. **De browser start de download** van het .eml-bestand
3. **Wacht tot de download is voltooid**

#### 3. Bewerken in Outlook
1. **Open het gedownloade .eml-bestand** (dubbelklik)
2. **Outlook opent** met een vooraf ingevulde e-mail:
   - Document als PDF-bijlage
   - Sjablooninhoud in de berichttekst
   - Ontvangersgegevens ingevuld
3. **Bewerk de e-mail** naar wens:
   - Onderwerpregel aanpassen
   - Persoonlijke tekst toevoegen
   - Extra bijlagen toevoegen
   - Opmaak aanpassen

#### 4. Verzenden
1. **Controleer uw e-mail**
2. **Klik op "Verzenden"** in Outlook
3. **De e-mail wordt verzonden** via uw persoonlijke Outlook-account
4. **De e-mail verschijnt** in uw Outlook-map "Verzonden items"

## Ondersteunde documenten

### Verkoopdocumenten
| Documenttype | Business Central-pagina | Beschikbare acties |
|--------------|------------------------|-------------------|
| **Verkoopoffertes** | Verkoopofferte (41, 42, 43) | E-mail verzenden → Bewerken in Outlook |
| **Verkooporders** | Verkooporder (44, 45, 46) | E-mail verzenden → Bewerken in Outlook |
| **Verkoopfacturen** | Verkoopfactuur (132, 133, 134) | E-mail verzenden → Bewerken in Outlook |
| **Geboekte verkoopfacturen** | Geboekte verkoopfactuur (132) | E-mail verzenden → Bewerken in Outlook |
| **Verkoopcreditnota's** | Verkoopcreditnota (114, 115) | E-mail verzenden → Bewerken in Outlook |

### Inkoopdocumenten
| Documenttype | Business Central-pagina | Beschikbare acties |
|--------------|------------------------|-------------------|
| **Inkoopoffertes** | Inkoopofferte (49, 50, 51) | E-mail verzenden → Bewerken in Outlook |
| **Inkooporders** | Inkooporder (52, 53, 54) | E-mail verzenden → Bewerken in Outlook |
| **Inkoopfacturen** | Inkoopfactuur (122, 123, 124) | E-mail verzenden → Bewerken in Outlook |
| **Inkoopcreditnota's** | Inkoopcreditnota (124, 125) | E-mail verzenden → Bewerken in Outlook |

### Magazijndocumenten
| Documenttype | Business Central-pagina | Beschikbare acties |
|--------------|------------------------|-------------------|
| **Magazijnverzendingen** | Magazijnverzending (7337) | E-mail verzenden → Bewerken in Outlook |
| **Geboekte magazijnverzendingen** | Geboekte magazijnverzending (7348) | E-mail verzenden → Bewerken in Outlook |

## Gebruikersinterface

### Business Central-e-maildialoogvenster
Wanneer u "E-mail verzenden" selecteert, ziet u:

![Dialoogvenster E-mail verzenden in Business Central](../../../assets/Send%20Email.png)

### Downloadprompt voor Edit in Outlook
Na het klikken op "Bewerken in Outlook":

```
┌─ Browserdownload ───────────────────────────┐
│ ⬇ Downloaden: Verkoopofferte_VO001.eml     │
│                                             │
│ ✓ Download voltooid                         │
│                                             │
│ [ Openen met Outlook ]  [ Weergeven in map ]│
└─────────────────────────────────────────────┘
```

### Outlook-opstelvenster
Het .eml-bestand opent in Outlook met:

```
┌─ Nieuw bericht - Outlook ───────────────────┐
│ Van: uw-e-mail@bedrijf.be                   │
│ Aan: klant@voorbeeld.be                     │
│ Onderwerp: Verkoopofferte VO001             │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Geachte klant,                          │ │
│ │                                         │ │
│ │ Bijgaand ontvangt u onze offerte VO001. │ │
│ │                                         │ │
│ │ Met vriendelijke groet,                 │ │
│ │ [Uw naam]                               │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Bijlagen: 📎 Verkoopofferte_VO001.pdf     │
│                                             │
│ [Verzenden] [Concept opslaan] [Verwijderen] │
└─────────────────────────────────────────────┘
```

## E-mailbewerkingsfuncties

### Tekstwijzigingen
In Outlook kunt u:
- **Onderwerpregel wijzigen**
- **Berichttekst aanpassen**:
  - Persoonlijke noot toevoegen
  - Sjabloontekst aanpassen
  - Opmaak aanpassen (vet, cursief, kleuren)
  - Lijsten toevoegen
  - Koppelingen invoegen

### Bijlagebeheer
- **Bestaande bijlagen bekijken** (PDF-document)
- **Extra bijlagen toevoegen**:
  - Aanvullende documenten
  - Afbeeldingen
  - Specificaties
  - Contracten
- **Bijlagen verwijderen** (indien nodig)
- **Bijlagen hernoemen**

### Ontvangers aanpassen
- **Veld Aan uitbreiden** met extra ontvangers
- **CC-ontvangers toevoegen**
- **BCC voor verborgen kopieën**
- **Adressen valideren** via het Outlook-adresboek

### Handtekening en opmaak
- **Persoonlijke handtekening** wordt automatisch toegevoegd
- **Bedrijfshuisstijl** behouden uit sjabloon
- **HTML-opmaak** volledig beschikbaar
- **Tekst met opmaak bewerken** via de Outlook-editor

## Geavanceerde functies

### Sjabloonpersonalisatie
Pas sjablonen aan per situatie:

```html
<!-- Voor verzending -->
<p>Geachte %CUSTOMER_NAME%,</p>
<p>Bijgaand ontvangt u %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Na bewerking in Outlook -->
<p>Geachte Jan Janssen,</p>
<p>Naar aanleiding van ons gesprek van vandaag ontvangt u bijgaand
onze herziene verkoopofferte VO001 met de bijgewerkte prijzen.</p>
```

### Bulk-e-mails bewerken
Voor meerdere documenten:
1. **Gebruik Edit in Outlook** voor het eerste document
2. **Sla op als sjabloon** in Outlook
3. **Pas het sjabloon toe** op volgende documenten
4. **Personaliseer** elk bericht

**Zie ook:** [Ondersteunde versies](supported-versions.md) | [Beperkingen](limitations.md)
