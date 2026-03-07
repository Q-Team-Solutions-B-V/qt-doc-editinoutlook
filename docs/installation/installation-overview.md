# Installation Overview

This page provides a complete overview of the installation and configuration of Edit in Outlook for Microsoft Dynamics 365 Business Central.

## Pre-requisites

### Business Central Requirements
- **Business Central version**: 27.0 or higher
- **Platform**: SaaS or On-Premise
- **User permissions**: Minimum Sales/Purchase user rights
- **Browser**: Modern browser with JavaScript support

### Microsoft Office Requirements  
- **Office 365**: Active Office 365 subscription
- **Outlook**: Outlook desktop app or Outlook Web Access
- **Exchange**: Exchange Online or Exchange Server 2016+

### Q-Team Dependencies
- **Q-Team App Authenticator**: Version 27.0.46044.0 or higher
- **License**: Valid Edit in Outlook license

## Installation Methods

### 1. SaaS Installation (AppSource)

#### Step 1: Find App in AppSource
1. Go to [Microsoft AppSource](https://appsource.microsoft.com/)
2. Search for "Q-Team Solutions Edit in Outlook"
3. Click "Get it now"

#### Step 2: Install App
1. Log in with your Business Central administrator account
2. Select your Business Central environment  
3. Confirm the installation
4. Wait for installation to complete (5-10 minutes)

#### Step 3: Verification
1. Open Business Central
2. Go to **Extension Management**
3. Check that "Edit In Outlook" shows status "Installed"

### 2. On-Premise Installation

#### Step 1: Download App
1. Visit [Q-Team Solutions website](https://www.q-teamsolutions.com/product/edit-in-outlook/)
2. Download the latest .app file
3. Save the file on your Business Central server

#### Step 2: Install App via Business Central Admin
1. Open **Business Central Administration Shell**
2. Execute the following command:
```powershell
Install-NAVApp -ServerInstance [InstanceName] -Path "[Path-to-app-file]"
```

#### Stap 3: App publiceren
```powershell
Publish-NAVApp -ServerInstance [InstanceName] -Name "Edit In Outlook" -Publisher "Q-Team Solutions"
```

#### Stap 4: Data upgrade (indien nodig)
```powershell
Start-NAVAppDataUpgrade -ServerInstance [InstanceName] -Name "Edit In Outlook" -Publisher "Q-Team Solutions"
```

## Post-Installatie Setup

### 1. Q-Team App Authenticator Setup
De Edit in Outlook app vereist Q-Team App Authenticator:

1. **Installeer Q-Team App Authenticator** (als nog niet geïnstalleerd)
2. **Configureer authenticatie**:
   - Ga naar Q-Team App Authenticator setup
   - Voer licentie gegevens in
   - Test de verbinding

### 2. Gebruikersrechten Toewijzen

#### Permission Sets
Wijs de juiste permission sets toe aan gebruikers:
- `QTEAM EIO USER` - Voor eindgebruikers
- `QTEAM EIO ADMIN` - Voor beheerders

#### Stappen:
1. Ga naar **Users** in Business Central
2. Selecteer een gebruiker
3. Ga naar **User Permission Sets**
4. Voeg `QTEAM EIO USER` toe

### 3. E-mail Account Setup

#### Business Central E-mail Setup
1. Ga naar **Email Accounts** in Business Central
2. Configureer SMTP settings (indien nog niet gedaan)
3. Test e-mail connectiviteit

**Belangrijk**: Met Edit in Outlook hoef je GEEN persoonlijke e-mailadressen toe te voegen aan Business Central.

## Configuratie

### Basis Configuratie

#### Edit in Outlook Setup Pagina
1. Zoek naar "Edit in Outlook Setup" 
2. Open de setup pagina
3. Configureer de volgende instellingen:

| Instelling | Beschrijving | Standaard |
|-----------|--------------|-----------|
| `Enable Edit in Outlook` | Schakel functionaliteit in | `Yes` |
| `Default Email Template` | Standaard template voor nieuwe e-mails | `''` |
| `Allow Attachment Download` | Sta toe dat gebruikers bijlagen downloaden | `Yes` |
| `PDF Preview Enabled` | Schakel PDF preview in | `Yes` |

### Geavancerde Configuratie

#### E-mail Templates
1. Ga naar **Email Templates**
2. Configeer templates voor verschillende document types
3. Test templates met Edit in Outlook functionaliteit

#### Document Layout Setup
1. **Report Selections**: Configureer welke rapporten gebruikt worden
2. **Layout Options**: Kies tussen verschillende lay-outs
3. **Template Assignment**: Wijs templates toe aan specifieke documenten

## Verificatie van Installatie

### Test Scenario
1. **Maak een Sales Quote**
2. **Klik op "Send Email"**  
3. **Selecteer "Edit in Outlook"**
4. **Controleer of .eml bestand wordt gedownload**
5. **Open bestand in Outlook**
6. **Verificeer dat alle data correct is**

### Mogelijke Test Cases
- Sales Quote → E-mail template → Edit in Outlook
- Purchase Order → Vendor e-mail → Edit in Outlook  
- Posted Invoice → Customer e-mail → Edit in Outlook

## Troubleshooting Installatie

### Veelvoorkomende Problemen

#### App niet zichtbaar na installatie
**Oplossing**:
1. Controleer Extension Management
2. Restart Business Central service (On-Premise)
3. Verifieer dependency op Q-Team Authenticator

#### Geen "Edit in Outlook" optie in e-mail dialoog
**Oplossing**:
1. Controleer gebruikersrechten
2. Verifieer app configuratie
3. Check browser JavaScript enabled

#### .eml bestand download faalt
**Oplossing**:
1. Controleer browser instellingen
2. Verifieer pop-up blocker settings
3. Test met andere browser

### Log Files
- **SaaS**: Gebruik Application Insights logs
- **On-Premise**: Check Event Viewer en Business Central logs

## Update Procedure

### SaaS Updates
- Automatische updates via Microsoft AppSource
- Gebruikers krijgen notificatie bij belangrijke updates

### On-Premise Updates  
1. Download nieuwe .app versie
2. Voer update procedure uit via Admin Shell
3. Test functionaliteit na update

---

**Volgende stappen:**
- [Office Add-in Installatie](office-addin-installation.md) - Installatiedetails
- [Configuratie](configuration.md) - Geavanceerde instellingen
- [Gebruik](../usage/editing-emails.md) - Hoe te gebruiken