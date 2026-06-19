# Editing Emails

This page describes how to use Edit in Outlook to edit and send Business Central document emails via Microsoft Outlook.

## Basic Workflow

### Step-by-Step Process

#### 1. Document Selection
1. **Open a Business Central document** (e.g. Sales Quote, Invoice, Order)
2. **Click on "Send Email"** action in the ribbon
3. **Email dialog opens**

#### 2. Activate Edit in Outlook
1. **In the email dialog**:
   - Select recipients
   - Choose email template (optional)
   - **Click on "Edit in Outlook"** button
2. **Browser starts download** of .eml file
3. **Wait until download completes**

#### 3. Outlook Editing
1. **Open downloaded .eml file** (double-click)
2. **Outlook opens** with pre-populated email:
   - Document as PDF attachment
   - Template content in email body
   - Recipient information filled in
3. **Edit email** as desired:
   - Adjust subject
   - Add personal text
   - Add extra attachments  
   - Adjust formatting

#### 4. Sending
1. **Review your email**
2. **Click "Send"** in Outlook
3. **Email is sent** via your personal Outlook account
4. **Email appears** in your Outlook "Sent Items"

## Ondersteunde Documenten

### Sales Documenten
| Document Type | Business Central Pagina | Beschikbare Acties |
|---------------|-------------------------|-------------------|
| **Sales Quotes** | Sales Quote (41, 42, 43) | Send Email → Edit in Outlook |
| **Sales Orders** | Sales Order (44, 45, 46) | Send Email → Edit in Outlook |
| **Sales Invoices** | Sales Invoice (132, 133, 134) | Send Email → Edit in Outlook |
| **Posted Sales Invoices** | Posted Sales Invoice (132) | Send Email → Edit in Outlook |
| **Sales Credit Memos** | Sales Credit Memo (114, 115) | Send Email → Edit in Outlook |

### Purchase Documenten  
| Document Type | Business Central Pagina | Beschikbare Acties |
|---------------|-------------------------|-------------------|
| **Purchase Quotes** | Purchase Quote (49, 50, 51) | Send Email → Edit in Outlook |
| **Purchase Orders** | Purchase Order (52, 53, 54) | Send Email → Edit in Outlook |
| **Purchase Invoices** | Purchase Invoice (122, 123, 124) | Send Email → Edit in Outlook |
| **Purchase Credit Memos** | Purchase Credit Memo (124, 125) | Send Email → Edit in Outlook |

### Warehouse Documenten
| Document Type | Business Central Pagina | Beschikbare Acties |
|---------------|-------------------------|-------------------|
| **Warehouse Shipments** | Warehouse Shipment (7337) | Send Email → Edit in Outlook |
| **Posted Whse. Shipments** | Posted Whse. Shipment (7348) | Send Email → Edit in Outlook |

## Gebruikersinterface

### Business Central E-mail Dialoog
Wanneer je "Send Email" selecteert, zie je:

![Send Email](../assets/Send%20Email.png)

### Edit in Outlook Download Prompt
Na het klikken op "Edit in Outlook":

![Download](../assets/Download.png)

### Outlook Compose Window
Het .eml bestand opent in Outlook met:

![New Message - Outlook](../assets/New%20Message%20-%20Outlook.png)

## E-mail Bewerking Mogelijkheden

### Tekst Aanpassingen
In Outlook kun je:
- **Subject line wijzigen**
- **Body tekst aanpassen**:
  - Persoonlijke noot toevoegen
  - Template tekst modificeren
  - Opmaak aanpassen (vet, cursief, kleuren)
  - Lijsten toevoegen
  - Links invoegen

### Bijlagen Beheer
- **Bestaande bijlagen bekijken** (PDF document)
- **Extra bijlagen toevoegen**:
  - Aanvullende documenten
  - Afbeeldingen
  - Specificaties
  - Contracten
- **Bijlagen verwijderen** (indien nodig)
- **Bijlagen hernoemen**

### Ontvangers Aanpassen
- **To veld uitbreiden** met extra ontvangers
- **Cc ontvangers toevoegen**
- **Bcc voor verborgen kopieën**
- **Adressen valideren** via Outlook address book

### Handtekening & Opmaak
- **Persoonlijke handtekening** wordt automatisch toegevoegd
- **Company branding** behouden uit template
- **HTML formatting** volledig beschikbaar
- **Rich text editing** met Outlook's editor

## Geavanceerde Features

### Template Personalisatie
Pas templates aan per situatie:
```html
<!-- Voordat verzending -->
<p>Dear %CUSTOMER_NAME%,</p>
<p>Please find attached %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Na bewerking in Outlook -->
<p>Dear John Smith,</p>
<p>Following our conversation today, please find attached 
our revised Sales Quote SQ001 with the updated pricing.</p>
```

### Bulk E-mail Bewerking
Voor meerdere documenten:
1. **Gebruik Edit in Outlook** voor eerste document
2. **Save als template** in Outlook
3. **Apply template** voor volgende documenten
4. **Personaliseer** elk bericht

### Follow-up Beheer
- **Set reminder** in Outlook voor follow-up
- **Categorize** e-mails voor organization
- **Flag for follow-up** met specific dates
- **Track** e-mail delivery en read receipts

## Best Practices

### Template Management
1. **Ontwikkel standaard templates** voor elk document type
2. **Test templates** met verschillende scenario's
3. **Train gebruikers** in template aanpassingen
4. **Maintain consistency** in company branding

### Persoonlijke Workflow
1. **Check e-mail content** voordat verzending
2. **Verify recipient addresses** zijn correct
3. **Add personal touch** waar gepast
4. **Archive sent items** systematisch

### Quality Control
1. **Preview PDF attachment** voordat verzending
2. **Spell check** je aangepaste tekst
3. **Test links** indien toegevoegd
4. **Verify formatting** op verschillende devices

## Mobiele Toegang

### Outlook Mobile
Edit in Outlook werkt ook via mobiele workflow:
1. **Download .eml** op desktop/laptop
2. **Sync** via OneDrive of e-mail naar jezelf
3. **Open in Outlook Mobile**
4. **Bewerk en verstuur** onderweg

### Cross-platform
- **Windows**: Native Outlook integratie
- **Mac**: Outlook for Mac ondersteuning  
- **Web**: Outlook Web Access compatibility
- **Mobile**: iOS en Android Outlook apps

---

**Volgende stappen:**
- [Ondersteunde Versies](supported-versions.md) - Compatibiliteit info
- [Beperkingen](limitations.md) - Wat te verwachten
- [FAQ](../faq/faq.md) - Veelgestelde vragen