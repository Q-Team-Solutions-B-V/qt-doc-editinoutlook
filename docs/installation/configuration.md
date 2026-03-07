# Configuration

This page describes all configuration options for the Q-Team Solutions Edit in Outlook app in Microsoft Dynamics 365 Business Central.

## Setup Page

### Access Configuration
1. **Search for "Edit in Outlook Setup"** in Business Central
2. **Open the setup page**
3. **Configure settings** according to organizational needs

### Basic Settings

#### Main Config Tab
| Field | Description | Default | Notes |
|-------|-------------|---------|-------|
| **Enable Edit in Outlook** | Enable/disable functionality | `Yes` | Master switch for all functionality |
| **Show in Email Dialog** | Show option in email dialog | `Yes` | Determines visibility of option |
| **Default Template Code** | Default template for new emails | `''` | Leave blank for system default |
| **Enable PDF Preview** | PDF preview in browser | `Yes` | Requires PDF viewer component |
| **Allow Custom Templates** | Users may create own templates | `No` | Security consideration |

#### Advanced Settings
| Field | Description | Default | Notes |
|-------|-------------|---------|-------|
| **Debug Mode** | Extended logging | `No` | For troubleshooting only |
| **Max File Size (MB)** | Maximum size of EML files | `25` | Browser/email client limits |
| **Session Timeout (Min)** | Control add-in timeout | `30` | Browser session management |
| **Enable Telemetry** | Analytics data collection | `Yes` | For support and improvement |

## Email Template Configuration

### Template Management
Edit in Outlook uses standard Business Central email templates with extensions.

#### Template Types
1. **Sales Document Templates**
   - Sales Quotes
   - Sales Orders  
   - Sales Invoices
   - Sales Credit Memos

2. **Purchase Document Templates**
   - Purchase Quotes
   - Purchase Orders
   - Purchase Invoices
   - Purchase Credit Memos

3. **Custom Templates**
   - User-defined templates
   - Department-specific templates
   - Customer-specific layouts

#### Template Configuration Steps
1. **Go to Email Templates** in Business Central
2. **Select relevant template**
3. **Edit template content**:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>%1</title> <!-- Document Type -->
   </head>
   <body>
       <h1>%2</h1>     <!-- Company Name -->
       <p>Dear %3,</p> <!-- Customer Name -->
       
       <p>Please find attached %4.</p> <!-- Document Description -->
       
       <p>Best regards,<br/>
       %5</p>          <!-- User Name -->
   </body>
   </html>
   ```

### Template Variables
Supported placeholders in templates:

| Variable | Description | Usage |
|----------|-------------|-------|
| `%1` | Document Type | Sales Quote, Invoice, etc. |
| `%2` | Company Name | Company name |
| `%3` | Customer/Vendor Name | Recipient name |
| `%4` | Document Description | "Sales Quote No. SQ001" |
| `%5` | User Name | Sender name |
| `%6` | Document Date | Document date |
| `%7` | Due Date | Due date (where relevant) |
| `%8` | Amount | Total amount |
| `%9` | Currency Code | Currency code |
| `%10` | Custom Field 1 | Configurable field |

## Document Type Configuration

### Report Selection Setup
Configure which reports are used for each document type:

#### Sales Documents
1. **Go to Report Selection - Sales**
2. **Configure for each Usage**:
   - `Email Body`: Template for email body
   - `Email Attachment`: PDF report for attachment
   - `Email Layout`: Layout-specific settings

#### Purchase Documents  
1. **Go to Report Selection - Purchase**
2. **Configure analogous to Sales**

#### Warehouse Documents
1. **Go to Report Selection - Warehouse**
2. **Configure shipment templates**

### Document Layout Options
| Document Type | Default Report | Layout Options |
|---------------|----------------|----------------|
| Sales Quote | Report 1304 | Standard, Detailed, Simple |
| Sales Order | Report 1305 | Standard, Packing Slip |
| Sales Invoice | Report 1306 | Standard, Detailed, Pro Forma |
| Purchase Order | Report 405 | Standard, Simplified |
| Warehouse Shipment | Report 5795 | Standard, Compact |

## User Permissions Configuration

### Permission Sets
The app contains various permission sets:

#### QTEAM EIO USER
**For**: End users
**Rights**:
- Read email templates
- Use Edit in Outlook functionality  
- Download EML files
- Basic document access

#### QTEAM EIO ADMIN
**For**: App administrators
**Rights**:
- All USER rights
- Configuration of setup page
- Template management
- Debug functionality
- User management

#### QTEAM EIO DEVELOPER
**For**: Developers/consultants
**Rights**:  
- All ADMIN rights
- Access to Integration Events
- Extensibility debugging
- Advanced telemetry

### User Assignment
Assign correct rights per user group:
```al
// Example: Bulk assignment via AL code
UserPermissionSets.SetRange("User ID", UserId);
UserPermissionSets.SetRange("Permission Set ID", 'QTEAM EIO USER');
if not UserPermissionSets.FindFirst() then begin
    UserPermissionSets.Init();
    UserPermissionSets."User ID" := UserId;
    UserPermissionSets."Permission Set ID" := 'QTEAM EIO USER';
    UserPermissionSets.Insert();
end;
```

## Environment-Specific Configuration

### Development Environment
For development environments:
```json
{
    "debugMode": true,
    "telemetryEnabled": false,
    "maxFileSizeMB": 10,
    "sessionTimeoutMin": 60
}
```

### Production Environment  
For production environments:
```json
{
    "debugMode": false,
    "telemetryEnabled": true,
    "maxFileSizeMB": 25,
    "sessionTimeoutMin": 30
}
```

### Test Environment
For test environments:
```json
{  
    "debugMode": true,
    "telemetryEnabled": true,
    "maxFileSizeMB": 50,
    "sessionTimeoutMin": 45
}
```

## Performance Configuration

### Browser Optimization
For better performance:

#### Control Add-in Settings
- **Lazy Loading**: Control add-ins load only when needed
- **Memory Management**: Automatic cleanup after use
- **Caching**: Template caching for faster loading

#### JavaScript Optimization
```javascript
// Browser detection and optimization
const browserConfig = {
    chrome: { 
        maxConcurrentDownloads: 5,
        memoryLimit: '100MB'
    },
    edge: { 
        maxConcurrentDownloads: 3,
        memoryLimit: '80MB'  
    },
    firefox: {
        maxConcurrentDownloads: 4,
        memoryLimit: '90MB'
    }
};
```

### Server Optimization
For Business Central server performance:

#### Codeunit Optimization
```al
// Example: Using temporary records for performance
TempEmailItem.DeleteAll();
EmailItem.SetRange("Document Type", DocumentType);
EmailItem.SetRange("Document No.", DocumentNo);
if EmailItem.FindSet() then
    repeat
        TempEmailItem := EmailItem;
        TempEmailItem.Insert();
    until EmailItem.Next() = 0;
```

## Security Configuration

### Data Protection
- **Personal Data**: GDPR compliance settings
- **Audit Trail**: Logging of email activity
- **Data Retention**: Automatic cleanup of temporary files

### Access Control
- **IP Restrictions**: Limit access to specific IP ranges
- **User Restrictions**: Limit functionality per user group  
- **Document Restrictions**: Limit access to specific document types

---

**Next steps:**
- [Editing emails](../usage/editing-emails.md) - Start using
- [API Overview](../integration/api-overview.md) - Integration possibilities
- [Common Errors](../troubleshooting/common-errors.md) - Problem solving
   - Department-specific templates
   - Customer-specific layouts

#### Template Configuratie Stappen
1. **Ga naar Email Templates** in Business Central
2. **Selecteer relevant template**
3. **Edit template content**:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>%1</title> <!-- Document Type -->
   </head>
   <body>
       <h1>%2</h1>     <!-- Company Name -->
       <p>Dear %3,</p> <!-- Customer Name -->
       
       <p>Please find attached %4.</p> <!-- Document Description -->
       
       <p>Best regards,<br/>
       %5</p>          <!-- User Name -->
   </body>
   </html>
   ```

### Template Variabelen
Ondersteunde placeholders in templates:

| Variabele | Beschrijving | Gebruik |
|-----------|--------------|---------|
| `%1` | Document Type | Sales Quote, Invoice, etc. |
| `%2` | Company Name | Naam van bedrijf |
| `%3` | Customer/Vendor Name | Ontvanger naam |
| `%4` | Document Description | "Sales Quote No. SQ001" |
| `%5` | User Name | Naam van verzender |
| `%6` | Document Date | Datum van document |
| `%7` | Due Date | Vervaldatum (waar relevant) |
| `%8` | Amount | Totaalbedrag |
| `%9` | Currency Code | Valuta code |
| `%10` | Custom Field 1 | Configureerbaar veld |

## Document Type Configuratie

### Report Selection Setup
Configureer welke rapporten gebruikt worden voor elk documenttype:

#### Sales Documents
1. **Ga naar Report Selection - Sales**
2. **Configureer voor elke Usage**:
   - `Email Body`: Template voor e-mail body
   - `Email Attachment`: PDF rapport voor bijlage
   - `Email Layout`: Layout specifieke instellingen

#### Purchase Documents  
1. **Ga naar Report Selection - Purchase**
2. **Configureer analoog aan Sales**

#### Warehouse Documents
1. **Ga naar Report Selection - Warehouse**
2. **Configureer shipment templates**

### Document Layout Options
| Document Type | Standaard Rapport | Layout Opties |
|---------------|------------------|---------------|
| Sales Quote | Report 1304 | Standard, Detailed, Simple |
| Sales Order | Report 1305 | Standard, Packing Slip |
| Sales Invoice | Report 1306 | Standard, Detailed, Pro Forma |
| Purchase Order | Report 405 | Standard, Simplified |
| Warehouse Shipment | Report 5795 | Standard, Compact |

## Gebruikersrechten Configuratie

### Permission Sets
De app bevat verschillende permission sets:

#### QTEAM EIO USER
**Voor**: Eindgebruikers
**Rechten**:
- Lezen van e-mail templates
- Gebruik van Edit in Outlook functionaliteit  
- Download van EML bestanden
- Basis document toegang

#### QTEAM EIO ADMIN
**Voor**: App beheerders
**Rechten**:
- Alle USER rechten
- Configuratie van setup pagina
- Template management
- Debug functionaliteit
- Gebruiker management

#### QTEAM EIO DEVELOPER
**Voor**: Ontwikkelaars/consultants
**Rechten**:  
- Alle ADMIN rechten
- Toegang tot Integration Events
- Extensibility debugging
- Advanced telemetry

### User Assignment
Wijs juiste rechten toe per gebruikersgroep:
```al
// Voorbeeld: Bulk toewijzing via AL code
UserPermissionSets.SetRange("User ID", UserId);
UserPermissionSets.SetRange("Permission Set ID", 'QTEAM EIO USER');
if not UserPermissionSets.FindFirst() then begin
    UserPermissionSets.Init();
    UserPermissionSets."User ID" := UserId;
    UserPermissionSets."Permission Set ID" := 'QTEAM EIO USER';
    UserPermissionSets.Insert();
end;
```

## Miljøspecifieke Configuratie

### Development Environment
Voor ontwikkelomgevingen:
```json
{
    "debugMode": true,
    "telemetryEnabled": false,
    "maxFileSizeMB": 10,
    "sessionTimeoutMin": 60
}
```

### Production Environment  
Voor productieomgevingen:
```json
{
    "debugMode": false,
    "telemetryEnabled": true,
    "maxFileSizeMB": 25,
    "sessionTimeoutMin": 30
}
```

### Test Environment
Voor testomgevingen:
```json
{  
    "debugMode": true,
    "telemetryEnabled": true,
    "maxFileSizeMB": 50,
    "sessionTimeoutMin": 45
}
```

## Performance Configuratie

### Browser Optimalisatie
Voor betere performance:

#### Control Add-in Settings
- **Lazy Loading**: Control add-ins laden only when needed
- **Memory Management**: Automatic cleanup na gebruik
- **Caching**: Template caching voor snellere loading

#### JavaScript Optimalisatie
```javascript
// Browser detection en optimalisatie
const browserConfig = {
    chrome: { 
        maxConcurrentDownloads: 5,
        memoryLimit: '100MB'
    },
    edge: { 
        maxConcurrentDownloads: 3,
        memoryLimit: '80MB'  
    },
    firefox: {
        maxConcurrentDownloads: 4,
        memoryLimit: '90MB'
    }
};
```

### Server Optimalisatie
Voor Business Central server performance:

#### Codeunit Optimalisatie
```al
// Voorbeeld: Gebruik van temporary records voor performance
TempEmailItem.DeleteAll();
EmailItem.SetRange("Document Type", DocumentType);
EmailItem.SetRange("Document No.", DocumentNo);
if EmailItem.FindSet() then
    repeat
        TempEmailItem := EmailItem;
        TempEmailItem.Insert();
    until EmailItem.Next() = 0;
```

## Security Configuratie

### Data Protection
- **Personal Data**: GDPR compliance instellingen
- **Audit Trail**: Logging van e-mail activiteit
- **Data Retention**: Automatische cleanup van tijdelijke bestanden

### Access Control
- **IP Restrictions**: Beperken toegang tot specifieke IP ranges
- **User Restrictions**: Beperken functionaliteit per gebruikersgroep  
- **Document Restrictions**: Beperken toegang tot specifieke documenttypen

---

**Volgende stappen:**
- [E-mails bewerken](../usage/editing-emails.md) - Start met gebruiken
- [API Overzicht](../integration/api-overview.md) - Integratie mogelijkheden
- [Common Errors](../troubleshooting/common-errors.md) - Probleemoplossing