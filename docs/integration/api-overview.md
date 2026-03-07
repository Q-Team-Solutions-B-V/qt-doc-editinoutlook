# API Overview

This page provides a comprehensive overview of the APIs, Integration Events and extensibility options of Edit in Outlook.

## Overview

Edit in Outlook offers various extensibility points for developers to extend functionality or adapt it to specific business requirements.

## Integration Events

### Email Functions Codeunit (ID: [YOUR_CODEUNIT_ID])

The core codeunit provides various Integration Events for custom implementations:

#### OnBeforeGenerateEML Event
**Usage**: Custom preprocessing before EML is generated
```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEML(EmailMessageId: Guid; var IsHandled: Boolean)
```

**Parameters**:
- `EmailMessageId`: Unique identifier for the email message
- `IsHandled`: Set to `true` to prevent default processing

**Example Implementation**:
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::[YOUR_EMAIL_FUNCTIONS_CODEUNIT], 'OnBeforeGenerateEML', '', false, false)]
local procedure OnBeforeGenerateEMLHandler(EmailMessageId: Guid; var IsHandled: Boolean)
var
    EmailMessage: Record "Email Message";
    CustomValidation: Codeunit "Custom Email Validation";
begin
    if EmailMessage.Get(EmailMessageId) then begin
        // Custom validation logic
        if not CustomValidation.ValidateMessage(EmailMessage) then begin
            Message('Custom validation failed');
            IsHandled := true;
        end;
    end;
end;
```

#### OnAfterGenerateEML Event
**Usage**: Post-processing after EML generation
```al
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEML(FileName: Text; FileContent: InStream)
```

**Parameters**:
- `FileName`: Name of the generated EML file
- `FileContent`: InStream with complete EML content

**Example Implementation**:
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::[YOUR_EMAIL_FUNCTIONS_CODEUNIT], 'OnAfterGenerateEML', '', false, false)]
local procedure OnAfterGenerateEMLHandler(FileName: Text; FileContent: InStream)
var
    EmailArchive: Codeunit "Email Archive Management";
    TempBlob: Codeunit "Temp Blob";
    OutStream: OutStream;
begin
    // Archive the EML file for compliance
    TempBlob.CreateOutStream(OutStream);
    CopyStream(OutStream, FileContent);
    
    EmailArchive.ArchiveEMLFile(FileName, TempBlob);
end;
```

### Document-Specific Events

#### Warehouse Shipment Events
For warehouse-specific EML generation:

```al
// Before warehouse shipment EML generation
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMLFilePostedShipment(var PostedWhseShipmentHeader: Record "Posted Whse. Shipment Header"; var IsHandled: Boolean)

// After warehouse shipment EML generation  
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEMLFilePostedShipment(FileName: Text; FileContent: InStream)

// Before active warehouse shipment EML
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMLFileShipment(var WarehouseShipmentHeader: Record "Warehouse Shipment Header"; var IsHandled: Boolean)

// After active warehouse shipment EML
[IntegrationEvent(false, false)]
local procedure OnAfterGenerateEMLFileShipment(FileName: Text; FileContent: InStream)
```

#### List Processing Events
For bulk/list processing:
```al
[IntegrationEvent(false, false)]
local procedure OnBeforeGenerateEMlFromList(var RecordRef: RecordRef; var IsHandled: Boolean)
```

## Control Add-in API

### JavaScript Interface

Edit in Outlook uses Control Add-ins for client-side functionality. These provide JavaScript APIs:

#### QTEAMEditInOutlookControlAdd
**Primary Interface**: Main control add-in for Edit in Outlook functionality

```javascript
// Control Add-in methods
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('DownloadEMLFile', [fileName, fileContent]);
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('ShowProgress', [message, percentage]);
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('HideProgress', []);
```

**AL Side Events**:
```al
// Event triggered from JavaScript
procedure OnEMLDownloadCompleted(FileName: Text; Success: Boolean)

// Event for progress updates
procedure OnProgressUpdate(Message: Text; Percentage: Integer)
```

#### QTEAMEmailDataControlAdd  
**Data Management**: For email data manipulation
```javascript
// Set email data
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('SetEmailData', [emailJson]);

// Get modified data
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('GetModifiedData', []);

// Validate email content
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('ValidateContent', [contentHtml]);
```

#### QTEAMDropAreaControl
**File Handling**: For drag-and-drop functionality
```javascript
// Handle file drops
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('HandleFileDrop', [fileArray]);

// Add attachment
Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('AddAttachment', [fileName, fileContent]);
```

## Custom Extensions

### Extension Development Pattern

#### 1. Create Extension App
```json
// app.json for custom extension
{
  "id": "12345678-1234-1234-1234-123456789abc",
  "name": "Custom Edit in Outlook Extensions",
  "publisher": "Your Company",
  "version": "1.0.0.0",
  "dependencies": [
    {
      "id": "0e9ac084-9f49-46d3-b3d1-224b4e7dba0a",
      "publisher": "Q-Team Solutions", 
      "name": "Edit In Outlook",
      "version": "27.0.46066.0"
    }
  ]
}
```

#### 2. Implement Event Subscribers
```al
codeunit 50100 "Custom EIO Integration"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::[YOUR_EMAIL_FUNCTIONS_ID], 'OnBeforeGenerateEML', '', false, false)]
    local procedure CustomPreProcessing(EmailMessageId: Guid; var IsHandled: Boolean)
    var
        CustomLogic: Codeunit "Custom Email Logic";
    begin
        CustomLogic.ProcessEmail(EmailMessageId);
        // Don't set IsHandled to true unless you want to replace default behavior
    end;
    
    [EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnAfterGenerateEML', '', false, false)]
    local procedure CustomPostProcessing(FileName: Text; FileContent: InStream)
    var
        EmailLogger: Codeunit "Email Activity Logger";
    begin
        EmailLogger.LogEMLGeneration(FileName, FileContent);
    end;
}
```

### Custom Template Engine

#### Example: Dynamic Template Selection
```al
codeunit 50101 "Dynamic Template Engine"
{
    procedure GetCustomTemplate(DocumentType: Enum "Document Type"; CustomerNo: Text): Text
    var
        Customer: Record Customer;
        EmailTemplate: Record "Email Template";
        TemplateCode: Text;
    begin
        if Customer.Get(CustomerNo) then begin
            // Logic: Select template based on customer category
            case Customer."Customer Category" of
                Customer."Customer Category"::VIP:
                    TemplateCode := 'VIP_' + Format(DocumentType);
                Customer."Customer Category"::Standard:
                    TemplateCode := 'STD_' + Format(DocumentType);
                else
                    TemplateCode := 'DEFAULT';
            end;
            
            if EmailTemplate.Get(TemplateCode) then
                exit(EmailTemplate."Body Content");
        end;
        
        // Fallback to default
        exit(GetDefaultTemplate(DocumentType));
    end;
}
```

## REST API Integration

### External System Integration

Although Edit in Outlook doesn't expose a direct REST API, you can integrate via Business Central APIs:

#### Business Central OData API
```http
GET /v2.0/companies({companyId})/emailTemplates
Authorization: Bearer {token}
Content-Type: application/json
```

**Response**:
```json
{
  "value": [
    {
      "code": "SALES_QUOTE",
      "description": "Sales Quote Template", 
      "bodyContent": "<html>...</html>",
      "subjectContent": "Quote %1 from %2"
    }
  ]
}
```

#### Custom API for EML Generation
```al
// Custom API Page for external integration
api page 50100 "EML Generation API"
{
    APIPublisher = 'YourCompany';
    APIGroup = 'EditInOutlook';
    APIVersion = 'v1.0';
    EntityName = 'emlGeneration';
    EntitySetName = 'emlGenerations';
    SourceTable = "Email Message";
    DelayedInsert = true;
    ChangeTrackingAllowed = true;
    
    layout
    {
        area(content)
        {
            field(messageId; Rec."Message Id") { }
            field(documentType; DocumentType) { }
            field(documentNo; DocumentNo) { }
            field(generateEML; GenerateEML) { }
        }
    }
    
    actions
    {
        area(Processing)
        {
            action(GenerateEmailFile)
            {
                trigger OnAction()
                var
                    EIOFunctions: Codeunit [YOUR_EMAIL_FUNCTIONS_CODEUNIT];
                begin
                    EIOFunctions.GenerateEMLFile(Rec."Message Id");
                end;
            }
        }
    }
}
```

## Webhooks & Real-time Integration

### Event Notification System

#### Custom Webhook Implementation
```al
codeunit 50102 "EIO Webhook Manager"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnAfterGenerateEML', '', false, false)]
    local procedure NotifyExternalSystem(FileName: Text; FileContent: InStream)
    var
        WebhookCall: Codeunit "Webhook Call Management";
        JsonPayload: JsonObject;
    begin
        JsonPayload.Add('fileName', FileName);
        JsonPayload.Add('timestamp', CurrentDateTime);
        JsonPayload.Add('status', 'generated');
        
        WebhookCall.SendNotification('edit-in-outlook-generated', JsonPayload);
    end;
}
```

## Database Extensions

### Custom Tables for Audit Trail

#### EML Generation Log
```al
table 50100 "EML Generation Log"
{
    DataClassification = CustomerContent;
    
    fields
    {
        field(1; "Entry No."; Integer)
        {
            DataClassification = SystemMetadata;
            AutoIncrement = true;
        }
        field(2; "Email Message ID"; Guid)
        {
            DataClassification = SystemMetadata;
        }
        field(3; "Generated DateTime"; DateTime)
        {
            DataClassification = CustomerContent;
        }
        field(4; "User ID"; Code[50])
        {
            DataClassification = CustomerContent;
            TableRelation = User."User Name";
        }
        field(5; "Document Type"; Text[50])
        {
            DataClassification = CustomerContent;
        }
        field(6; "Document No."; Code[20])
        {
            DataClassification = CustomerContent;
        }
        field(7; "File Size"; Integer)
        {
            DataClassification = CustomerContent;
        }
        field(8; "Success"; Boolean)
        {
            DataClassification = CustomerContent;
        }
    }
    
    keys
    {
        key(PK; "Entry No.") { Clustered = true; }
        key(MessageID; "Email Message ID") { }
        key(DateTime; "Generated DateTime") { }
    }
}
```

## Testing & Debugging API

### Debug Mode Functions

#### Enable Debug Logging
```al
codeunit 50103 "EIO Debug Helper"
{
    procedure EnableDebugMode()
    var
        EIOSetup: Record "QTEAM EIO Setup";
    begin
        if EIOSetup.Get() then begin
            EIOSetup."Debug Mode" := true;
            EIOSetup.Modify();
        end;
    end;
    
    procedure LogDebugMessage(Message: Text; Data: Variant)
    var
        TempBlob: Codeunit "Temp Blob";
        OutStream: OutStream;
    begin
        if not IsDebugModeEnabled() then
            exit;
            
        TempBlob.CreateOutStream(OutStream);
        OutStream.WriteText(StrSubstNo('%1: %2 - %3', CurrentDateTime, Message, Format(Data)));
        
        // Log to Application Insights or file
        LogToSystem(TempBlob);
    end;
}
```

---

**Next steps:**
- [Authentication](authentication.md) - Security integration
- [Troubleshooting](../troubleshooting/common-errors.md) - Common issues and solutions