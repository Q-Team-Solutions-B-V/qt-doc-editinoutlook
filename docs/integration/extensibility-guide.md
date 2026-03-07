# Q-Team Solutions Edit in Outlook - Extensibility Guide

## Overview

The **Q-Team Solutions Edit in Outlook** extension for Microsoft Dynamics 365 Business Central provides various capabilities for third parties to extend the functionality. This document describes all available Integration Events and other extensibility points.

## Integration Events

The app provides various Integration Events that allow third parties to customize or extend functionality:

### QTEAMEIOEmailFunctions Codeunit (ID: 11196255)

#### OnBeforeGenerateEML
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 552)

```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEML(EmailMessageId: Guid; var IsHandled: Boolean)
```

**Purpose:** Called before an EML file is generated
**Parameters:**
- `EmailMessageId`: GUID of the email message
- `IsHandled`: Set to `true` to prevent default processing

**Usage:** Implement custom logic for EML generation or add extra validations.

#### OnAfterGenerateEML
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 572)

```al
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEML(FileName: Text; FileContent: Instream)
```

**Purpose:** Called after an EML file has been generated
**Parameters:**
- `FileName`: Name of the generated file
- `FileContent`: InStream with the file content

**Usage:** Perform post-processing on generated EML files, such as logging or archiving.

#### OnBeforeGenerateEMLFilePostedShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 557)

```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMLFilePostedShipment(var OnBeforeGenerateEMLFilePostedShipment: Record "Posted Whse. Shipment Header"; var IsHandled: Boolean)
```

**Purpose:** Called before an EML file is generated for a posted warehouse shipment
**Parameters:**
- `OnBeforeGenerateEMLFilePostedShipment`: Record of the posted warehouse shipment
- `IsHandled`: Set to `true` to prevent default processing

**Usage:** Implement custom logic for warehouse shipment emails.

#### OnAfterGenerateEMLFilePostedShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 577)

```al
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEMLFilePostedShipment(FileName: Text; FileContent: Instream)
```

**Purpose:** Called after an EML file has been generated for a posted warehouse shipment
**Parameters:**
- `FileName`: Name of the generated file
- `FileContent`: InStream with the file content

#### OnBeforeGenerateEMLFileShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 562)

```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMLFileShipment(var WarehouseShipmentHeader: Record "Warehouse Shipment Header"; var IsHandled: Boolean)
```

**Purpose:** Called before an EML file is generated for a warehouse shipment
**Parameters:**
- `WarehouseShipmentHeader`: Record of the warehouse shipment
- `IsHandled`: Set to `true` to prevent default processing

#### OnAfterGenerateEMLFileShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 582)

```al
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEMLFileShipment(FileName: Text; FileContent: Instream)
```

**Purpose:** Called after an EML file has been generated for a warehouse shipment
**Parameters:**
- `FileName`: Name of the generated file
- `FileContent`: InStream with the file content

#### OnBeforeGenerateEMlFromList
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 567)

```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMlFromList(RecVariant: Variant; ReportSelectionUsage: Enum "Report Selection Usage"; Subject: Text; ToEmail: Text; var IsHandled: Boolean)
```

**Purpose:** Called before an EML is generated from a list
**Parameters:**
- `RecVariant`: Variant of the record
- `ReportSelectionUsage`: Enum for report selection usage
- `Subject`: Email subject
- `ToEmail`: Email address of recipient
- `IsHandled`: Set to `true` to prevent default processing

#### OnAfterGenerateEMLFromList
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 587)

```al
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEMLFromList(FileName: Text; FileContent: Instream)
```

**Purpose:** Called after an EML has been generated from a list
**Parameters:**
- `FileName`: Name of the generated file
- `FileContent`: InStream with the file content

## Public Procedures

The app provides various public procedures that can be called by third parties:

### QTEAMEIOEmailFunctions Codeunit

#### GenerateEMLFileEmailFromEditor
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 3)

```al
procedure GenerateEMLFileEmailFromEditor(VariantRecRef: Variant; ReportUsage: Integer)
```

**Purpose:** Generates an EML file from the email editor
**Parameters:**
- `VariantRecRef`: Variant of a record reference
- `ReportUsage`: Integer for report usage

#### GenerateEMLV2
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 106)

```al
procedure GenerateEMLV2(EmailMessageId: Guid)
```

**Purpose:** Generates an EML file (version 2)
**Parameters:**
- `EmailMessageId`: GUID of the email message

#### GenerateEML
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 165)

```al
procedure GenerateEML(VariantRecRef: Variant; ReportUsage: Integer; EmailSubject: Text)
```

**Purpose:** Generates an EML file
**Parameters:**
- `VariantRecRef`: Variant of a record reference
- `ReportUsage`: Integer for report usage
- `EmailSubject`: Email subject

#### GenerateEMLFile
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 217)

```al
procedure GenerateEMLFile(var QTEAMEIOEmailItem: Record "QTEAM EIO Email Item")
```

**Purpose:** Generates an EML file from an email item
**Parameters:**
- `QTEAMEIOEmailItem`: Record of QTEAM EIO Email Item

#### GenerateEMLFilePostedShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 299)

```al
procedure GenerateEMLFilePostedShipment(var PostedWhseShipmentHeader: Record "Posted Whse. Shipment Header")
```

**Purpose:** Generates an EML file for a posted warehouse shipment
**Parameters:**
- `PostedWhseShipmentHeader`: Record of the posted warehouse shipment header

#### GenerateEMLFileShipment
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 368)

```al
procedure GenerateEMLFileShipment(var WarehouseShipmentHeader: Record "Warehouse Shipment Header")
```

**Purpose:** Generates an EML file for a warehouse shipment
**Parameters:**
- `WarehouseShipmentHeader`: Record of the warehouse shipment header

#### GenerateEMlFromList
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 437)

```al
procedure GenerateEMlFromList(RecVariant: Variant; ReportSelectionUsage: Enum "Report Selection Usage"; Subject: Text; ToEmail: Text) BodyText: Text
```

**Purpose:** Generates an EML from a list and returns the body text
**Parameters:**
- `RecVariant`: Variant of the record
- `ReportSelectionUsage`: Enum for report selection usage
- `Subject`: Email subject
- `ToEmail`: Email address of recipient
**Returns:** Body text of the email

#### GetReportInformation
**Location:** `src/codeunit/QTEAMEIOEmailFunctions.codeunit.al` (line 509)

```al
procedure GetReportInformation(var ReportId: Integer; var EmailBodyLayoutName: Text[250]; ReportSelectionUsage: Enum "Report Selection Usage"; IsAttachment: Boolean)
```

**Purpose:** Retrieves report information
**Parameters:**
- `ReportId`: Report ID (by reference)
- `EmailBodyLayoutName`: Name of the email body layout (by reference)
- `ReportSelectionUsage`: Enum for report selection usage
- `IsAttachment`: Boolean indicating if it's an attachment

### QTEAMEIOEmailItemSession Codeunit

#### ProcessEmailItemInBackground
**Location:** `src/codeunit/QTEAMEIOEmailItemSession.codeunit.al` (line 22)

```al
procedure ProcessEmailItemInBackground(UserId: Text; DocumentNo: Code[20]; DocumentType: Integer; DocumentRecordId: RecordId)
```

**Purpose:** Processes an email item in the background
**Parameters:**
- `UserId`: User ID
- `DocumentNo`: Document number
- `DocumentType`: Document type
- `DocumentRecordId`: Record ID of the document

### PDF Viewer Procedures

#### LoadPdfViaUrl (QTEAMPDFViewer)
**Location:** `src/page/QTEAMPDFViewer.page.al` (line 48)

```al
procedure LoadPdfViaUrl(Url: Text)
```

**Purpose:** Loads a PDF via a URL
**Parameters:**
- `Url`: URL to the PDF file

#### LoadPdfFromBlob (QTEAMPDFViewer)
**Location:** `src/page/QTEAMPDFViewer.page.al` (line 55)

```al
procedure LoadPdfFromBlob(Base64Data: Text)
```

**Purpose:** Loads a PDF from Base64-encoded data
**Parameters:**
- `Base64Data`: Base64-encoded PDF data

### DropArea Procedures

#### SetData (QTEAMDropArea)
**Location:** `src/page/QTEAMDropArea.page.al` (lines 49 and 56)

```al
procedure SetData(EmailMessageId: Guid);
procedure SetData(CustomerId: Code[20]; TableId: Integer);
```

**Purpose:** Sets data for the DropArea functionality
**Parameters:**
- Overload 1: `EmailMessageId` - GUID of the email message
- Overload 2: `CustomerId` - Customer ID and `TableId` - Table ID

## Event Subscribers

The app uses various Event Subscribers that modify how standard Business Central functionality works:

### SaveSalesEmailItem
**Location:** `src/codeunit/QTEAMEditinOutlookSubs.codeunit.al` (line 6)

Subscribes to: `Table "Report Selections".'OnBeforeSendEmailToCust'`

**Purpose:** Saves sales email item before standard email is sent

### SavePurchasingEmailItem
**Location:** `src/codeunit/QTEAMEditinOutlookSubs.codeunit.al` (line 36)

Subscribes to: `Table "Report Selections".'OnBeforeSendEmailToVendor'`

**Purpose:** Saves purchasing email item before standard email is sent

### AddInfoToEmailOutbox
**Location:** `src/codeunit/QTEAMEditinOutlookSubs.codeunit.al` (line 17)

Subscribes to: `Page "Email Editor".'OnAfterGetRecordEvent'`

**Purpose:** Adds extra information to the email outbox

### OnBeforeSendDocumentSendingProfile
**Location:** `src/codeunit/QTEAMEditinOutlookSubs.codeunit.al` (line 47)

Subscribes to: `Table "Document Sending Profile".OnAfterSend`

**Purpose:** Handles documents sent via Outlook

## Tables and Data Structure

The app introduces several new tables that can be used by third parties:

### QTEAM EIO Email Item
**Purpose:** Stores email item information for Edit in Outlook functionality

### QTEAM Email Message
**Purpose:** Stores email message data

### QTEAM Email Message Attachment
**Purpose:** Stores attachments for email messages

### QTEAM PDF Viewer Setup
**Purpose:** Configuration for PDF viewer functionality

## Permission Sets

The app provides various permission sets for different license levels:
- **QTEAMEIOEssentials**: Basic permissions for Essential license
- **QTEAMEIOPremium**: Extended permissions for Premium license
- **QTEAMProductKey**: Permissions for product key functionality

## Implementation Guidelines

### Event Subscriber Implementation

To subscribe to the Integration Events, create an Event Subscriber codeunit:

```al
codeunit 50000 "My EIO Extension"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::"QTEAM EIO Email Functions", 'OnBeforeGenerateEML', '', false, false)]
    local procedure OnBeforeGenerateEML(EmailMessageId: Guid; var IsHandled: Boolean)
    begin
        // Your custom logic here
        // Set IsHandled to true to prevent default processing
    end;

    [EventSubscriber(ObjectType::Codeunit, Codeunit::"QTEAM EIO Email Functions", 'OnAfterGenerateEML', '', false, false)]
    local procedure OnAfterGenerateEML(FileName: Text; FileContent: Instream)
    begin
        // Post-processing logic here
    end;
}
```

### Calling Public Procedures

```al
codeunit 50001 "My EIO Usage"
{
    procedure GenerateCustomEmail()
    var
        QTEAMEmailFunctions: Codeunit "QTEAM EIO Email Functions";
        SalesHeader: Record "Sales Header";
    begin
        // Get your record
        SalesHeader.Get(SalesHeader."Document Type"::Order, 'SO001');
        
        // Call public procedure
        QTEAMEmailFunctions.GenerateEML(SalesHeader, 1, 'Custom Subject');
    end;
}
```

## Best Practices

1. **Event Handling**: Always use the `IsHandled` parameter correctly in Before-events
2. **Error Handling**: Implement proper error handling in your event subscribers
3. **Performance**: Consider performance when implementing event subscribers
4. **Testing**: Test your implementations thoroughly, especially when overriding default behavior
5. **Dependencies**: Make sure your extension has the correct dependencies on the QT Edit in Outlook app

## Usage Examples

### Custom Email Body Modification

```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::"QTEAM EIO Email Functions", 'OnAfterGenerateEML', '', false, false)]
local procedure CustomizeEmailBody(FileName: Text; FileContent: Instream)
var
    TempBlob: Codeunit "Temp Blob";
    OutStream: OutStream;
    InStream: InStream;
    EmailContent: Text;
begin
    // Read current content
    FileContent.ReadText(EmailContent);
    
    // Add custom content
    EmailContent := EmailContent + '<p>Custom footer content</p>';
    
    // Write back (implementation depends on your needs)
end;
```

### Custom Validation

```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::"QTEAM EIO Email Functions", 'OnBeforeGenerateEMLFromList', '', false, false)]
local procedure ValidateBeforeGeneration(RecVariant: Variant; ReportSelectionUsage: Enum "Report Selection Usage"; Subject: Text; ToEmail: Text; var IsHandled: Boolean)
var
    SalesHeader: Record "Sales Header";
begin
    // Validate if email address is valid
    if ToEmail = '' then begin
        Message('Email address is required');
        IsHandled := true;
        exit;
    end;
    
    // Add extra business logic
end;
```

## Contact and Support

For more information about extending the Q-Team Solutions Edit in Outlook app, contact:

**Q-Team Solutions**
- Website: [www.q-teamsolutions.com](https://www.q-teamsolutions.com)
- Email: support@q-teamsolutions.com

---

*This document is based on version 27.2.45889.1 of the Q-Team Solutions Edit in Outlook extension.*