# Office Add-in Installation

This page describes the specific steps for installing and configuring the Office components needed for Edit in Outlook.

## Overview

Edit in Outlook does not use a traditional Outlook add-in, but works via EML files that are opened directly in Outlook. This approach offers maximum compatibility and requires no special Office add-in installation.

## EML File Association

### Windows File Association

#### Automatic Configuration
Most Windows systems automatically have the correct file association:
- `.eml` files → Microsoft Outlook
- Double-clicking opens directly in Outlook

#### Manual Configuration (if needed)
1. **Right-click on .eml file**
2. **Select "Open with" → "Choose another app"**
3. **Select Microsoft Outlook**
4. **Check: "Always use this app to open .eml files"**
5. **Click OK**

#### Via Windows Settings
1. **Open Windows Settings** (`Win + I`)
2. **Go to Apps → Default apps**
3. **Scroll to "Choose default apps by file type"**
4. **Search for `.eml`**
5. **Select Microsoft Outlook**

### Alternative: Via Registry (Advanced)
```registry
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.eml\OpenWithList]
"a"="OUTLOOK.EXE"
"MRUList"="a"

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.eml\UserChoice]
"ProgId"="Microsoft.Outlook.EML"
```

## Browser Configuration

### Download Location
For optimal workflow, configure your browser download settings:

#### Chrome
1. **Go to Settings** (`chrome://settings/`)
2. **Advanced → Downloads**
3. **Set download location** (e.g. `C:\Users\[Username]\Downloads\EditInOutlook\`)
4. **Optional**: Disable "Ask where to save each file before downloading"

#### Edge
1. **Go to Settings** (`edge://settings/`)
2. **Downloads**
3. **Configure download path**
4. **Optional**: Disable "Ask me what to do with each download"

#### Firefox
1. **Go to Settings** (`about:preferences`)
2. **General → Files and Applications**
3. **Set download folder**
4. **Configure .eml file action to "Open with Microsoft Outlook"**

### Pop-up Blocker
Ensure that Business Central is not blocked:

#### Chrome Pop-up Settings
1. **Go to** `chrome://settings/content/popups`
2. **Add your Business Central URL** to "Allowed to show pop-ups and redirects"

#### Edge Pop-up Settings
1. **Go to** `edge://settings/content/popups`  
2. **Add Business Central domain** to exceptions

## Outlook Configuration

### Outlook Desktop App

#### Email Account Setup
Ensure Outlook is properly configured:
1. **Office 365 account** active and working
2. **Send/Receive** functions correctly
3. **Test email sending** works

#### Outlook Settings
For optimal experience:
1. **File → Options → Mail**
2. **Compose messages**: HTML format (recommended)
3. **Message format**: Rich Text or HTML
4. **Winmail.dat prevention**: Configure to HTML/Plain Text for external recipients

#### Signature Setup
1. **File → Options → Mail → Signatures**
2. **Configure personal signature**
3. **Set as default** for new messages
4. **Test signature** with Edit in Outlook workflow

### Outlook Web Access (OWA)

#### Browser Configuration
For OWA usage:
1. **Ensure your default browser** has Outlook Web Access as default for `.eml`
2. **Test .eml file opening** in web browser
3. **Configure OWA notifications** for new messages

## Multi-User Installation

### Domain Environment Setup

#### Group Policy Configuration
For organizations with Group Policy:

```xml
<!-- Registry.pol configuration for .eml association -->
<RegistrySettings>
    <Registry>
        <Key>HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.eml</Key>
        <ValueName>(Default)</ValueName>
        <Value>Microsoft.Outlook.EML</Value>
        <Type>REG_SZ</Type>
    </Registry>
</RegistrySettings>
```

#### Deployment Script
PowerShell script for bulk deployment:
```powershell
# Set EML file association to Outlook
$progId = "Microsoft.Outlook.EML"
$extension = ".eml"

# Set file association
cmd /c "assoc $extension=$progId"
cmd /c "ftype $progId=`"C:\Program Files\Microsoft Office\root\Office16\OUTLOOK.EXE`" /eml `"%1`""

Write-Host "EML file association configured for Outlook"
```

### User Training Script
PowerShell script to help users:
```powershell
# Test EML association
$emlTest = "C:\temp\test.eml"
$testContent = @"
From: test@example.com
To: user@example.com  
Subject: Test EML File
Content-Type: text/plain

This is a test EML file for Edit in Outlook.
"@

$testContent | Out-File -FilePath $emlTest -Encoding ASCII

# Test file opening
Start-Process $emlTest
Write-Host "Test EML file created and opened. Verify it opens in Outlook."
```

## Troubleshooting Office Integration

### Common Problems

#### .EML does not open in Outlook
**Causes**:
- Incorrect file association  
- Outlook not installed
- Multiple email clients installed

**Solutions**:
1. **Reinstall Outlook** as dominant email client
2. **Repair Office installation** via Control Panel
3. **Reset file associations** via Windows Settings

#### Browser download problems
**Causes**:
- Pop-up blocker
- Download restrictions
- Antivirus interference

**Solutions**:
1. **Whitelist Business Central** in browser
2. **Configure antivirus** to allow .eml downloads
3. **Test different browser** for troubleshooting

#### Outlook opens message incorrectly
**Causes**:
- Encoding problems
- Template formatting issues
- Attachment corruption

**Solutions**:
1. **Check character encoding** in EML files
2. **Verify template HTML** is valid
3. **Test with minimal template** for debugging

### Diagnostic Tools

#### Browser Developer Tools
For debugging browser issues:
1. **Open Developer Tools** (F12)
2. **Check Console** for JavaScript errors
3. **Monitor Network tab** for download failures
4. **Inspect Application tab** for storage issues

#### Windows Event Viewer
For system-level troubleshooting:
1. **Open Event Viewer**
2. **Check Applications and Services Logs**
3. **Look for Outlook-related** errors
4. **Monitor file association** events

---

**Next steps:**
- [Configuration](configuration.md) - App configuration details
- [Editing emails](../usage/editing-emails.md) - User guide
- [Troubleshooting](../troubleshooting/common-errors.md) - Problem solving

Deze pagina beschrijft de specifieke stappen voor het installeren en configureren van de Office componenten die nodig zijn voor Edit in Outlook.

## Overzicht

Edit in Outlook gebruikt geen traditionele Outlook add-in, maar werkt via EML bestanden die direct geopend worden in Outlook. Deze aanpak biedt maximale compatibiliteit en vereist geen speciale Office add-in installatie.

## EML Bestand Associatie

### Windows Bestandsassociatie

#### Automatische Configuratie
De meeste Windows systemen hebben automatisch de juiste bestandsassociatie:
- `.eml` bestanden → Microsoft Outlook
- Dubbelklikken opent direct in Outlook

#### Handmatige Configuratie (indien nodig)
1. **Rechtsklik op .eml bestand**
2. **Selecteer "Open with" → "Choose another app"**
3. **Selecteer Microsoft Outlook**
4. **Vink aan: "Always use this app to open .eml files"**
5. **Klik OK**

#### Via Windows Settings
1. **Open Windows Settings** (`Win + I`)
2. **Ga naar Apps → Default apps**
3. **Scroll naar "Choose default apps by file type"**
4. **Zoek naar `.eml`**
5. **Selecteer Microsoft Outlook**

### Alternative: Via Registry (Advanced)
```registry
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.eml\OpenWithList]
"a"="OUTLOOK.EXE"
"MRUList"="a"

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.eml\UserChoice]
"ProgId"="Microsoft.Outlook.EML"
```

## Browser Configuratie

### Download Locatie
Voor optimale workflow configureer je browser download instellingen:

#### Chrome
1. **Ga naar Settings** (`chrome://settings/`)
2. **Advanced → Downloads**
3. **Stel download locatie in** (bijv. `C:\Users\[Username]\Downloads\EditInOutlook\`)
4. **Optioneel**: Schakel "Ask where to save each file before downloading" uit

#### Edge
1. **Ga naar Settings** (`edge://settings/`)
2. **Downloads**
3. **Configureer download pad**
4. **Optioneel**: "Ask me what to do with each download" uitschakelen

#### Firefox
1. **Ga naar Settings** (`about:preferences`)
2. **General → Files and Applications**
3. **Stel download folder in**
4. **Configureer .eml bestand actie naar "Open with Microsoft Outlook"**

### Pop-up Blocker
Zorg ervoor dat Business Central niet geblokkeerd wordt:

#### Chrome Pop-up Settings
1. **Ga naar** `chrome://settings/content/popups`
2. **Add je Business Central URL** naar "Allowed to show pop-ups and redirects"

#### Edge Pop-up Settings
1. **Ga naar** `edge://settings/content/popups`  
2. **Add Business Central domain** naar exceptions

## Outlook Configuratie

### Outlook Desktop App

#### E-mail Account Setup
Zorg dat Outlook correct geconfigureerd is:
1. **Office 365 account** actief en werkend
2. **Send/Receive** functioneert correct
3. **Test e-mail verzending** werkt

#### Outlook Instellingen
Voor optimale ervaring:
1. **File → Options → Mail**
2. **Compose messages**: HTML format (aanbevolen)
3. **Message format**: Rich Text of HTML
4. **Winmail.dat prevention**: Configureer naar HTML/Plain Text voor externe ontvangers

#### Handtekening Setup
1. **File → Options → Mail → Signatures**
2. **Configureer persoonlijke handtekening**
3. **Stel in als standaard** voor nieuwe berichten
4. **Test handtekening** met Edit in Outlook workflow

### Outlook Web Access (OWA)

#### Browser Configuratie
Voor OWA usage:
1. **Zorg dat je standaard browser** Outlook Web Access als default heeft voor `.eml`
2. **Test .eml file opening** in web browser
3. **Configureer OWA notifications** voor niewe berichten

## Multi-User Installatie

### Domain Environment Setup

#### Group Policy Configuration
Voor organisaties met Group Policy:

```xml
<!-- Registry.pol configuratie voor .eml associatie -->
<RegistrySettings>
    <Registry>
        <Key>HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.eml</Key>
        <ValueName>(Default)</ValueName>
        <Value>Microsoft.Outlook.EML</Value>
        <Type>REG_SZ</Type>
    </Registry>
</RegistrySettings>
```

#### Deployment Script
PowerShell script voor bulk deployment:
```powershell
# Set EML file association to Outlook
$progId = "Microsoft.Outlook.EML"
$extension = ".eml"

# Set file association
cmd /c "assoc $extension=$progId"
cmd /c "ftype $progId=`"C:\Program Files\Microsoft Office\root\Office16\OUTLOOK.EXE`" /eml `"%1`""

Write-Host "EML file association configured for Outlook"
```

### User Training Script
PowerShell script om gebruikers te helpen:
```powershell
# Test EML association
$emlTest = "C:\temp\test.eml"
$testContent = @"
From: test@example.com
To: user@example.com  
Subject: Test EML File
Content-Type: text/plain

This is a test EML file for Edit in Outlook.
"@

$testContent | Out-File -FilePath $emlTest -Encoding ASCII

# Test file opening
Start-Process $emlTest
Write-Host "Test EML file created and opened. Verify it opens in Outlook."
```

## Troubleshooting Office Integration

### Veelvoorkomende Problemen

#### .EML opent niet in Outlook
**Oorzaken**:
- Onjuiste bestandsassociatie  
- Outlook niet geïnstalleerd
- Meerdere e-mail clients geïnstalleerd

**Oplossingen**:
1. **Herinstalleer Outlook** als dominant e-mail client
2. **Repair Office installation** via Control Panel
3. **Reset bestandsassociaties** via Windows Settings

#### Browser download problemen
**Oorzaken**:
- Pop-up blocker
- Download restrictions
- Antivirus interference

**Oplossingen**:
1. **Whitelist Business Central** in browser
2. **Configure antivirus** to allow .eml downloads
3. **Test different browser** voor troubleshooting

#### Outlook opent bericht incorrectly
**Oorzaken**:
- Encoding problemen
- Template formatting issues
- Attachment corruption

**Oplossingen**:
1. **Check character encoding** in EML files
2. **Verify template HTML** is geldig
3. **Test met minimal template** voor debugging

### Diagnostics Tools

#### Browser Developer Tools
Voor debugging browser issues:
1. **Open Developer Tools** (F12)
2. **Check Console** voor JavaScript errors
3. **Monitor Network tab** voor download failures
4. **Inspect Application tab** voor storage issues

#### Windows Event Viewer
Voor systeem-level troubleshooting:
1. **Open Event Viewer**
2. **Check Applications and Services Logs**
3. **Look for Outlook-related** errors
4. **Monitor file association** events

---

**Volgende stappen:**
- [Configuratie](configuration.md) - App configuratie details
- [E-mails bewerken](../usage/editing-emails.md) - Gebruikshandleiding
- [Troubleshooting](../troubleshooting/common-errors.md) - Probleemoplossing