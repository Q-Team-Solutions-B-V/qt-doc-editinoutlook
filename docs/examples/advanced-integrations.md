# Advanced Integrations - Edit in Outlook

This document provides advanced examples and integration patterns for the Edit in Outlook functionality in Business Central.

## Advanced Email Templates and Automation

### Example 1: Dynamic Content Generation with Data Binding

```al
codeunit 50101 "Advanced EIO Templates"
{
    procedure CreateDynamicInvoiceEmail(SalesInvoiceHeader: Record "Sales Invoice Header"): Guid
    var
        EmailMessage: Record "Email Message";
        TemplateEngine: Codeunit "Q-Team Template Engine";
        EmailId: Guid;
    begin
        EmailId := CreateGuid();
        
        EmailMessage.Init();
        EmailMessage.Id := EmailId;
        EmailMessage.Subject := TemplateEngine.ProcessTemplate('INVOICE_SUBJECT', GetInvoiceTemplateData(SalesInvoiceHeader));
        EmailMessage.Body := TemplateEngine.ProcessTemplate('INVOICE_BODY', GetInvoiceTemplateData(SalesInvoiceHeader));
        EmailMessage."To Recipients" := GetCustomerEmail(SalesInvoiceHeader."Sell-to Customer No.");
        EmailMessage.Insert();
        
        // Add dynamic attachments
        AddDynamicAttachments(EmailMessage, SalesInvoiceHeader);
        
        exit(EmailId);
    end;
    
    local procedure GetInvoiceTemplateData(SalesInvoiceHeader: Record "Sales Invoice Header"): Text
    var
        Customer: Record Customer;
        SalesInvoiceLine: Record "Sales Invoice Line";
        TemplateData: JsonObject;
        LinesArray: JsonArray;
        LineObject: JsonObject;
        DataText: Text;
    begin
        Customer.Get(SalesInvoiceHeader."Sell-to Customer No.");
        
        // Build template data object
        TemplateData.Add('INVOICE_NO', SalesInvoiceHeader."No.");
        TemplateData.Add('CUSTOMER_NAME', Customer.Name);
        TemplateData.Add('CUSTOMER_EMAIL', Customer."E-Mail");
        TemplateData.Add('INVOICE_DATE', Format(SalesInvoiceHeader."Document Date"));
        TemplateData.Add('DUE_DATE', Format(SalesInvoiceHeader."Due Date"));
        TemplateData.Add('TOTAL_AMOUNT', Format(SalesInvoiceHeader."Amount Including VAT"));
        TemplateData.Add('CURRENCY_CODE', SalesInvoiceHeader."Currency Code");
        TemplateData.Add('COMPANY_NAME', CompanyName);
        
        // Add invoice lines
        SalesInvoiceLine.SetRange("Document No.", SalesInvoiceHeader."No.");
        if SalesInvoiceLine.FindSet() then
            repeat
                Clear(LineObject);
                LineObject.Add('DESCRIPTION', SalesInvoiceLine.Description);
                LineObject.Add('QUANTITY', Format(SalesInvoiceLine.Quantity));
                LineObject.Add('UNIT_PRICE', Format(SalesInvoiceLine."Unit Price"));
                LineObject.Add('LINE_AMOUNT', Format(SalesInvoiceLine."Line Amount"));
                LinesArray.Add(LineObject);
            until SalesInvoiceLine.Next() = 0;
        
        TemplateData.Add('INVOICE_LINES', LinesArray);
        
        TemplateData.WriteTo(DataText);
        exit(DataText);
    end;
}
```

### Example 2: Workflow-Based Email Automation

```al
codeunit 50102 "EIO Workflow Integration"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::"Workflow Management", 'OnExecuteWorkflowStep', '', false, false)]
    local procedure OnExecuteWorkflowStep(WorkflowStep: Record "Workflow Step"; var HandlerExecuted: Boolean)
    var
        WorkflowStepArgument: Record "Workflow Step Argument";
        RecRef: RecordRef;
        EmailId: Guid;
    begin
        if WorkflowStep."Function Name" = 'SEND_EIO_EMAIL' then begin
            WorkflowStepArgument.Get(WorkflowStep.Argument);
            RecRef.Get(WorkflowStep."Record ID");
            
            EmailId := CreateWorkflowEmail(RecRef, WorkflowStepArgument);
            
            if WorkflowStepArgument."Send for Approval" then
                SendForApproval(EmailId, RecRef)
            else
                OpenInOutlookForEditing(EmailId);
            
            HandlerExecuted := true;
        end;
    end;
    
    local procedure CreateWorkflowEmail(RecRef: RecordRef; WorkflowStepArgument: Record "Workflow Step Argument"): Guid
    var
        EmailMessage: Record "Email Message";
        EmailId: Guid;
    begin
        EmailId := CreateGuid();
        
        EmailMessage.Init();
        EmailMessage.Id := EmailId;
        EmailMessage.Subject := BuildWorkflowSubject(RecRef, WorkflowStepArgument);
        EmailMessage.Body := BuildWorkflowBody(RecRef, WorkflowStepArgument);
        EmailMessage."To Recipients" := GetWorkflowRecipients(RecRef, WorkflowStepArgument);
        EmailMessage.Insert();
        
        AttachWorkflowDocuments(EmailMessage, RecRef);
        
        exit(EmailId);
    end;
}
```

## Complex Control Add-in Scenarios

### Example 3: Rich Text Editor Integration

```html
<!DOCTYPE html>
<html>
<head>
    <title>Advanced Email Editor</title>
    <link href="https://cdn.quilljs.com/1.3.6/quill.snow.css" rel="stylesheet">
    <style>
        .editor-container {
            height: 500px;
            border: 1px solid #ccc;
        }
        
        .toolbar-custom {
            background-color: #f8f9fa;
            border-bottom: 1px solid #e9ecef;
            padding: 10px;
        }
        
        .template-selector {
            margin: 10px 0;
        }
        
        .recipient-manager {
            margin: 10px 0;
            padding: 10px;
            border: 1px solid #dee2e6;
        }
    </style>
</head>
<body>
    <div class="toolbar-custom">
        <select id="templateSelector" class="template-selector" onchange="loadTemplate()">
            <option value="">Select Template...</option>
            <option value="invoice">Invoice Template</option>
            <option value="quote">Quote Template</option>
            <option value="reminder">Payment Reminder</option>
        </select>
        
        <button onclick="saveAsDraft()" class="btn btn-secondary">Save Draft</button>
        <button onclick="sendEmail()" class="btn btn-primary">Send</button>
        <button onclick="exportToOutlook()" class="btn btn-success">Export to Outlook</button>
    </div>
    
    <div class="recipient-manager">
        <label>To:</label>
        <input type="text" id="toRecipients" placeholder="Enter email addresses">
        <button onclick="addCC()">Add CC</button>
        <button onclick="addBCC()">Add BCC</button>
        <div id="ccContainer" style="display:none;">
            <label>CC:</label>
            <input type="text" id="ccRecipients" placeholder="CC recipients">
        </div>
        <div id="bccContainer" style="display:none;">
            <label>BCC:</label>
            <input type="text" id="bccRecipients" placeholder="BCC recipients">
        </div>
    </div>
    
    <div>
        <input type="text" id="emailSubject" placeholder="Email Subject" style="width: 100%; margin: 5px 0; padding: 8px;">
    </div>
    
    <div id="editor" class="editor-container"></div>
    
    <script src="https://cdn.quilljs.com/1.3.6/quill.min.js"></script>
    <script src="AdvancedEmailEditor.js"></script>
</body>
</html>
```

```javascript
// AdvancedEmailEditor.js
class AdvancedEmailEditor {
    constructor() {
        this.initializeEditor();
        this.templates = {};
        this.attachments = [];
    }
    
    initializeEditor() {
        // Initialize Quill rich text editor
        this.quill = new Quill('#editor', {
            theme: 'snow',
            modules: {
                toolbar: [
                    [{'header': [1, 2, false]}],
                    ['bold', 'italic', 'underline', 'strike'],
                    [{'color': []}, {'background': []}],
                    [{'list': 'ordered'}, {'list': 'bullet'}],
                    [{'align': []}],
                    ['link', 'image'],
                    ['clean']
                ]
            }
        });
        
        // Notify Business Central that the editor is ready
        this.notifyReady();
    }
    
    notifyReady() {
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('EditorReady');
        }
    }
    
    loadEmailData(emailDataJson) {
        try {
            const emailData = JSON.parse(emailDataJson);
            
            document.getElementById('toRecipients').value = emailData.to || '';
            document.getElementById('emailSubject').value = emailData.subject || '';
            
            if (emailData.ccRecipients) {
                document.getElementById('ccRecipients').value = emailData.ccRecipients;
                document.getElementById('ccContainer').style.display = 'block';
            }
            
            if (emailData.bccRecipients) {
                document.getElementById('bccRecipients').value = emailData.bccRecipients;
                document.getElementById('bccContainer').style.display = 'block';
            }
            
            // Set rich text content
            this.quill.setContents(emailData.body || '');
            
            // Load attachments
            if (emailData.attachments) {
                this.attachments = emailData.attachments;
            }
            
        } catch (error) {
            console.error('Error loading email data:', error);
        }
    }
    
    loadTemplate() {
        const templateId = document.getElementById('templateSelector').value;
        if (!templateId) return;
        
        // Request template from Business Central
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('LoadTemplate', [templateId]);
        }
    }
    
    setTemplate(templateData) {
        try {
            const template = JSON.parse(templateData);
            
            document.getElementById('emailSubject').value = template.subject || '';
            this.quill.setContents(template.body || '');
            
        } catch (error) {
            console.error('Error setting template:', error);
        }
    }
    
    saveAsDraft() {
        const emailData = this.getEmailData();
        emailData.isDraft = true;
        
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('SaveDraft', [JSON.stringify(emailData)]);
        }
    }
    
    sendEmail() {
        const emailData = this.getEmailData();
        emailData.send = true;
        
        if (this.validateEmail(emailData)) {
            if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
                Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('SendEmail', [JSON.stringify(emailData)]);
            }
        }
    }
    
    exportToOutlook() {
        const emailData = this.getEmailData();
        
        // Create EML file content
        const emlContent = this.generateEMLContent(emailData);
        
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('ExportToOutlook', [emlContent]);
        }
    }
    
    getEmailData() {
        return {
            to: document.getElementById('toRecipients').value,
            cc: document.getElementById('ccRecipients').value,
            bcc: document.getElementById('bccRecipients').value,
            subject: document.getElementById('emailSubject').value,
            body: this.quill.getContents(),
            htmlBody: this.quill.root.innerHTML,
            attachments: this.attachments
        };
    }
    
    validateEmail(emailData) {
        if (!emailData.to || !emailData.subject) {
            alert('Please enter at least a recipient and subject.');
            return false;
        }
        
        // Validate email addresses
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        const toEmails = emailData.to.split(',').map(e => e.trim());
        
        for (let email of toEmails) {
            if (!emailRegex.test(email)) {
                alert(`Invalid email address: ${email}`);
                return false;
            }
        }
        
        return true;
    }
    
    generateEMLContent(emailData) {
        // Generate RFC 2822 compliant EML content
        let eml = `From: ${this.getFromAddress()}\r\n`;
        eml += `To: ${emailData.to}\r\n`;
        
        if (emailData.cc) eml += `Cc: ${emailData.cc}\r\n`;
        if (emailData.bcc) eml += `Bcc: ${emailData.bcc}\r\n`;
        
        eml += `Subject: ${emailData.subject}\r\n`;
        eml += `Date: ${new Date().toUTCString()}\r\n`;
        eml += `MIME-Version: 1.0\r\n`;
        eml += `Content-Type: text/html; charset=UTF-8\r\n`;
        eml += `Content-Transfer-Encoding: 7bit\r\n\r\n`;
        eml += emailData.htmlBody;
        
        return eml;
    }
    
    addCC() {
        document.getElementById('ccContainer').style.display = 'block';
        document.getElementById('ccRecipients').focus();
    }
    
    addBCC() {
        document.getElementById('bccContainer').style.display = 'block';
        document.getElementById('bccRecipients').focus();
    }
}

// Global functions for AL interaction
let advancedEditor;

window.addEventListener('load', function() {
    advancedEditor = new AdvancedEmailEditor();
});

function loadEmailData(emailDataJson) {
    if (advancedEditor) {
        advancedEditor.loadEmailData(emailDataJson);
    }
}

function setTemplate(templateData) {
    if (advancedEditor) {
        advancedEditor.setTemplate(templateData);
    }
}

function saveAsDraft() {
    if (advancedEditor) {
        advancedEditor.saveAsDraft();
    }
}

function sendEmail() {
    if (advancedEditor) {
        advancedEditor.sendEmail();
    }
}

function exportToOutlook() {
    if (advancedEditor) {
        advancedEditor.exportToOutlook();
    }
}
```

## Integration with External Systems

### Example 4: CRM Integration for Contact Management

```al
codeunit 50103 "EIO CRM Integration"
{
    procedure SyncEmailWithCRM(EmailMessageId: Guid)
    var
        EmailMessage: Record "Email Message";
        CRMConnection: Record "CRM Connection Setup";
        HttpClient: HttpClient;
        HttpRequest: HttpRequestMessage;
        HttpResponse: HttpResponseMessage;
        RequestBody: Text;
    begin
        if not EmailMessage.Get(EmailMessageId) then
            exit;
        
        if not CRMConnection.Get() then
            exit;
        
        RequestBody := BuildCRMSyncPayload(EmailMessage);
        
        HttpRequest.SetRequestUri(CRMConnection."Server Address" + '/api/emails');
        HttpRequest.Method := 'POST';
        HttpRequest.Content.WriteFrom(RequestBody);
        
        // Add authentication headers
        AddCRMAuthHeaders(HttpRequest, CRMConnection);
        
        if HttpClient.Send(HttpRequest, HttpResponse) then
            LogCRMSyncResult(EmailMessageId, HttpResponse.HttpStatusCode)
        else
            Error('Failed to sync email with CRM');
    end;
    
    local procedure BuildCRMSyncPayload(EmailMessage: Record "Email Message"): Text
    var
        JsonPayload: JsonObject;
        PayloadText: Text;
    begin
        JsonPayload.Add('subject', EmailMessage.Subject);
        JsonPayload.Add('body', EmailMessage.Body);
        JsonPayload.Add('to_recipients', EmailMessage."To Recipients");
        JsonPayload.Add('created_date', Format(EmailMessage.SystemCreatedAt));
        JsonPayload.Add('bc_message_id', Format(EmailMessage.Id));
        
        JsonPayload.WriteTo(PayloadText);
        exit(PayloadText);
    end;
}
```

### Example 5: Document Management System Integration

```al
codeunit 50104 "EIO Document Management"
{
    procedure ArchiveEmailWithDocuments(EmailMessageId: Guid)
    var
        EmailMessage: Record "Email Message";
        EmailAttachment: Record "Email Message Attachment";
        DMSConnection: Record "Document Management Setup";
        ArchiveResponse: Text;
    begin
        if not EmailMessage.Get(EmailMessageId) then
            exit;
        
        // Create document set in DMS
        ArchiveResponse := CreateDMSDocumentSet(EmailMessage);
        
        // Archive attachments
        EmailAttachment.SetRange("Email Message Id", EmailMessageId);
        if EmailAttachment.FindSet() then
            repeat
                ArchiveAttachmentInDMS(EmailAttachment, ArchiveResponse);
            until EmailAttachment.Next() = 0;
        
        // Update email record with archive reference
        EmailMessage."External Archive ID" := ExtractArchiveId(ArchiveResponse);
        EmailMessage.Modify();
    end;
    
    local procedure CreateDMSDocumentSet(EmailMessage: Record "Email Message"): Text
    var
        HttpClient: HttpClient;
        HttpRequest: HttpRequestMessage;
        HttpResponse: HttpResponseMessage;
        RequestPayload: JsonObject;
        RequestText: Text;
        ResponseText: Text;
    begin
        RequestPayload.Add('title', EmailMessage.Subject);
        RequestPayload.Add('type', 'EMAIL_CORRESPONDENCE');
        RequestPayload.Add('source', 'BUSINESS_CENTRAL');
        RequestPayload.Add('created_by', UserId());
        RequestPayload.Add('created_date', Format(CurrentDateTime()));
        
        RequestPayload.WriteTo(RequestText);
        
        HttpRequest.Content.WriteFrom(RequestText);
        HttpRequest.Method := 'POST';
        HttpRequest.SetRequestUri(GetDMSEndpoint() + '/document-sets');
        
        if HttpClient.Send(HttpRequest, HttpResponse) then begin
            HttpResponse.Content.ReadAs(ResponseText);
            exit(ResponseText);
        end else
            Error('Failed to create document set in DMS');
    end;
}
```

## Performance Optimization Patterns

### Example 6: Asynchronous Email Processing

```al
codeunit 50105 "EIO Async Processing"
{
    procedure QueueEmailForProcessing(EmailMessageId: Guid; ProcessingType: Enum "EIO Processing Type")
    var
        JobQueueEntry: Record "Job Queue Entry";
        JobQueueMgmt: Codeunit "Job Queue Management";
    begin
        JobQueueEntry.Init();
        JobQueueEntry.ID := CreateGuid();
        JobQueueEntry."Object Type to Run" := JobQueueEntry."Object Type to Run"::Codeunit;
        JobQueueEntry."Object ID to Run" := Codeunit::"EIO Background Processor";
        JobQueueEntry."Job Queue Category Code" := 'EIO-PROCESSING';
        JobQueueEntry."Parameter String" := Format(EmailMessageId) + '|' + Format(ProcessingType);
        JobQueueEntry.Description := 'Edit in Outlook: ' + GetProcessingDescription(ProcessingType);
        JobQueueEntry."Earliest Start Date/Time" := CurrentDateTime();
        JobQueueEntry.Insert(true);
        
        JobQueueMgmt.StartJob(JobQueueEntry, false);
    end;
    
    local procedure GetProcessingDescription(ProcessingType: Enum "EIO Processing Type"): Text
    begin
        case ProcessingType of
            ProcessingType::EmailGeneration:
                exit('Email Generation');
            ProcessingType::AttachmentProcessing:
                exit('Attachment Processing');
            ProcessingType::ExternalSync:
                exit('External System Sync');
        end;
    end;
}

codeunit 50106 "EIO Background Processor"
{
    TableNo = "Job Queue Entry";
    
    trigger OnRun()
    var
        Parameters: List of [Text];
        EmailMessageId: Guid;
        ProcessingType: Enum "EIO Processing Type";
    begin
        Parameters := Rec."Parameter String".Split('|');
        
        if Parameters.Count() >= 2 then begin
            Evaluate(EmailMessageId, Parameters.Get(1));
            Evaluate(ProcessingType, Parameters.Get(2));
            
            ProcessEmailInBackground(EmailMessageId, ProcessingType);
        end;
    end;
    
    local procedure ProcessEmailInBackground(EmailMessageId: Guid; ProcessingType: Enum "EIO Processing Type")
    var
        EmailProcessor: Codeunit "Q-Team EIO Email Functions";
        NotificationMgmt: Codeunit "EIO Notification Management";
    begin
        case ProcessingType of
            ProcessingType::EmailGeneration:
                begin
                    EmailProcessor.GenerateEMLFile(EmailMessageId);
                    NotificationMgmt.NotifyEmailReady(EmailMessageId);
                end;
            ProcessingType::AttachmentProcessing:
                begin
                    EmailProcessor.ProcessAllAttachments(EmailMessageId);
                    NotificationMgmt.NotifyAttachmentsReady(EmailMessageId);
                end;
            ProcessingType::ExternalSync:
                begin
                    SyncWithExternalSystems(EmailMessageId);
                    NotificationMgmt.NotifySyncCompleted(EmailMessageId);
                end;
        end;
    end;
}
```

### Example 7: Caching and Memory Optimization

```al
codeunit 50107 "EIO Cache Management"
{
    var
        TemplateCache: Dictionary of [Text, Text];
        AttachmentCache: Dictionary of [Guid, Text];
        CacheExpiry: Dictionary of [Text, DateTime];
        
    procedure GetCachedTemplate(TemplateCode: Text): Text
    var
        CachedTemplate: Text;
        ExpiryTime: DateTime;
    begin
        if CacheExpiry.Get(TemplateCode, ExpiryTime) then
            if ExpiryTime < CurrentDateTime() then begin
                // Cache expired, remove entries
                TemplateCache.Remove(TemplateCode);
                CacheExpiry.Remove(TemplateCode);
            end;
        
        if TemplateCache.Get(TemplateCode, CachedTemplate) then
            exit(CachedTemplate);
        
        // Load template and cache it
        CachedTemplate := LoadTemplateFromDatabase(TemplateCode);
        TemplateCache.Set(TemplateCode, CachedTemplate);
        CacheExpiry.Set(TemplateCode, CurrentDateTime() + (1000 * 60 * 30)); // 30 minutes
        
        exit(CachedTemplate);
    end;
    
    procedure ClearCache()
    begin
        Clear(TemplateCache);
        Clear(AttachmentCache);
        Clear(CacheExpiry);
    end;
    
    procedure GetCacheStatistics(): Text
    var
        Stats: Text;
    begin
        Stats := 'EIO Cache Statistics:\n';
        Stats += 'Template Cache Entries: ' + Format(TemplateCache.Count()) + '\n';
        Stats += 'Attachment Cache Entries: ' + Format(AttachmentCache.Count()) + '\n';
        Stats += 'Cache Expiry Entries: ' + Format(CacheExpiry.Count()) + '\n';
        
        exit(Stats);
    end;
}
```

---

**Next Steps:**
- [Sample Configuration](sample-config.md) - Complete setup examples and best practices
- [Basic Examples](basic-example.md) - Simpler implementation patterns
- [API Documentation](../api/api-overview.md) - Technical API reference