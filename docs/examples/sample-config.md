# Sample Configuration - Edit in Outlook

This document provides complete configuration examples and setup templates for the Edit in Outlook functionality.

## Complete App Configuration

### Example 1: app.json Configuration

```json
{
  "id": "12345678-1234-1234-1234-123456789012",
  "name": "Edit In Outlook",
  "publisher": "Q-Team Solutions",
  "version": "27.2.45889.1",
  "brief": "Enhanced email editing capabilities for Business Central",
  "description": "Edit emails directly in Microsoft Outlook with Business Central integration",
  "privacyStatement": "https://www.q-teamsolutions.com/privacy",
  "EULA": "https://www.q-teamsolutions.com/eula",
  "help": "https://docs.q-teamsolutions.com/edit-in-outlook",
  "url": "https://www.q-teamsolutions.com/edit-in-outlook",
  "logo": "assets/EditInOutlookLogo.png",
  "dependencies": [
    {
      "id": "63ca2fa4-4f03-4f2b-a480-172fef340d3f",
      "publisher": "Microsoft",
      "name": "System Application",
      "version": "27.0.0.0"
    },
    {
      "id": "437dbf0e-84ff-417a-965d-ed2bb9650972",
      "publisher": "Microsoft", 
      "name": "Base Application",
      "version": "27.0.0.0"
    },
    {
      "id": "88b7902e-1655-4e7b-9b04-824706b9a6d4",
      "publisher": "Q-Team Solutions",
      "name": "Q-Team App Authenticator",
      "version": "27.0.46066.0"
    }
  ],
  "screenshots": [
    "assets/screenshot1.png",
    "assets/screenshot2.png",
    "assets/screenshot3.png"
  ],
  "platform": "27.0.0.0",
  "application": "27.0.0.0",
  "idRanges": [
    {
      "from": 50000,
      "to": 50099
    }
  ],
  "resourceExposurePolicy": {
    "allowDebugging": false,
    "allowDownloadingSource": false,
    "includeSourceInSymbolFile": false
  },
  "features": [
    "NoImplicitWith"
  ],
  "runtime": "12.0",
  "target": "Cloud"
}
```

### Example 2: Permission Set Configuration

```xml
<!-- extensionsPermissionSet.xml -->
<PermissionSets>
  <PermissionSet RoleID="EDIT-IN-OUTLOOK" RoleName="Edit in Outlook User">
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>50000</ObjectID>  <!-- Q-Team EIO Setup -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>No</InsertPermission>
      <ModifyPermission>No</ModifyPermission>
      <DeletePermission>No</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>50001</ObjectID>  <!-- Q-Team Email Template -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>No</InsertPermission>
      <ModifyPermission>No</ModifyPermission>
      <DeletePermission>No</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>8900</ObjectID>   <!-- Email Message -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>8901</ObjectID>   <!-- Email Message Attachment -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>Codeunit</ObjectType>
      <ObjectID>50000</ObjectID>  <!-- Q-Team EIO Management -->
      <ExecutePermission>Yes</ExecutePermission>
    </Permission>
    
    <Permission>
      <ObjectType>Codeunit</ObjectType>
      <ObjectID>50001</ObjectID>  <!-- Q-Team EIO Email Functions -->
      <ExecutePermission>Yes</ExecutePermission>
    </Permission>
    
    <Permission>
      <ObjectType>Page</ObjectType>
      <ObjectID>50000</ObjectID>  <!-- Q-Team EIO Setup -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>No</InsertPermission>
      <ModifyPermission>No</ModifyPermission>
      <DeletePermission>No</DeletePermission>
    </Permission>
  </PermissionSet>
  
  <PermissionSet RoleID="EDIT-IN-OUTLOOK-ADMIN" RoleName="Edit in Outlook Administrator">
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>50000</ObjectID>  <!-- Q-Team EIO Setup -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>TableData</ObjectType>
      <ObjectID>50001</ObjectID>  <!-- Q-Team Email Template -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>Page</ObjectType>
      <ObjectID>50000</ObjectID>  <!-- Q-Team EIO Setup -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
    
    <Permission>
      <ObjectType>Page</ObjectType>
      <ObjectID>50001</ObjectID>  <!-- Q-Team Email Templates -->
      <ReadPermission>Yes</ReadPermission>
      <InsertPermission>Yes</InsertPermission>
      <ModifyPermission>Yes</ModifyPermission>
      <DeletePermission>Yes</DeletePermission>
    </Permission>
  </PermissionSet>
</PermissionSets>
```

## Email Template Configurations

### Example 3: Sales Invoice Template

```al
procedure CreateSalesInvoiceTemplate(): Code[20]
var
    EmailTemplate: Record "Q-Team Email Template";
    TemplateCode: Code[20];
begin
    TemplateCode := 'SALES-INVOICE';
    
    if EmailTemplate.Get(TemplateCode) then
        EmailTemplate.Delete(true);
    
    EmailTemplate.Init();
    EmailTemplate.Code := TemplateCode;
    EmailTemplate.Description := 'Sales Invoice Email Template';
    EmailTemplate.Subject := 'Invoice {INVOICE_NO} - {CUSTOMER_NAME}';
    EmailTemplate.Body := GetSalesInvoiceTemplateBody();
    EmailTemplate."Attachment Required" := true;
    EmailTemplate."Default Attachment Type" := EmailTemplate."Default Attachment Type"::PDF;
    EmailTemplate."Auto-Add Recipients" := true;
    EmailTemplate."CC Recipients" := 'accounting@company.com';
    EmailTemplate."Template Type" := EmailTemplate."Template Type"::Sales;
    EmailTemplate.Insert();
    
    exit(TemplateCode);
end;

local procedure GetSalesInvoiceTemplateBody(): Text
begin
    exit('Dear {CUSTOMER_NAME},\n\n' +
         'Thank you for your business. Please find attached invoice {INVOICE_NO} dated {INVOICE_DATE}.\n\n' +
         'Invoice Details:\n' +
         '- Invoice Number: {INVOICE_NO}\n' +
         '- Date: {INVOICE_DATE}\n' +
         '- Due Date: {DUE_DATE}\n' +
         '- Amount: {TOTAL_AMOUNT} {CURRENCY_CODE}\n\n' +
         'Payment can be made using the following methods:\n' +
         '- Bank Transfer: {BANK_ACCOUNT}\n' +
         '- Online Payment: {PAYMENT_LINK}\n\n' +
         'If you have any questions about this invoice, please contact us at {CONTACT_EMAIL}.\n\n' +
         'Best regards,\n' +
         '{SENDER_NAME}\n' +
         '{COMPANY_NAME}\n' +
         'Phone: {COMPANY_PHONE}\n' +
         'Email: {COMPANY_EMAIL}');
end;
```

### Example 4: Purchase Order Template

```al
procedure CreatePurchaseOrderTemplate(): Code[20]
var
    EmailTemplate: Record "Q-Team Email Template";
    TemplateCode: Code[20];
begin
    TemplateCode := 'PURCHASE-ORDER';
    
    EmailTemplate.Init();
    EmailTemplate.Code := TemplateCode;
    EmailTemplate.Description := 'Purchase Order Email Template';
    EmailTemplate.Subject := 'Purchase Order {PO_NUMBER} - {VENDOR_NAME}';
    EmailTemplate.Body := GetPurchaseOrderTemplateBody();
    EmailTemplate."Attachment Required" := true;
    EmailTemplate."Default Attachment Type" := EmailTemplate."Default Attachment Type"::PDF;
    EmailTemplate."Template Type" := EmailTemplate."Template Type"::Purchase;
    EmailTemplate."Require Approval" := true;
    EmailTemplate."Approval Required Amount" := 10000;
    EmailTemplate.Insert();
    
    exit(TemplateCode);
end;

local procedure GetPurchaseOrderTemplateBody(): Text
begin
    exit('Dear {VENDOR_NAME},\n\n' +
         'We would like to place the following order with your company.\n\n' +
         'Purchase Order Details:\n' +
         '- PO Number: {PO_NUMBER}\n' +
         '- Order Date: {ORDER_DATE}\n' +
         '- Expected Delivery: {EXPECTED_DELIVERY_DATE}\n' +
         '- Delivery Address: {DELIVERY_ADDRESS}\n\n' +
         'Order Items:\n' +
         '{ORDER_LINES}\n\n' +
         'Total Order Value: {TOTAL_AMOUNT} {CURRENCY_CODE}\n\n' +
         'Please confirm receipt of this order and provide an estimated delivery date.\n\n' +
         'Terms and Conditions:\n' +
         '- Payment Terms: {PAYMENT_TERMS}\n' +
         '- Delivery Terms: {DELIVERY_TERMS}\n\n' +
         'Contact Information:\n' +
         'Purchasing Department: {PURCHASING_EMAIL}\n' +
         'Phone: {PURCHASING_PHONE}\n\n' +
         'Best regards,\n' +
         '{SENDER_NAME}\n' +
         '{COMPANY_NAME}');
end;
```

## Control Add-in Configuration

### Example 5: Control Add-in Manifest

```al
controladdin "Q-Team EIO Email Editor"
{
    RequestedHeight = 600;
    MinimumHeight = 400;
    MaximumHeight = 1000;
    RequestedWidth = 800;
    MinimumWidth = 600;
    MaximumWidth = 1200;
    VerticalStretch = true;
    HorizontalStretch = true;
    VerticalShrink = true;
    HorizontalShrink = true;
    
    Scripts = 
        'js/EmailEditor.js',
        'js/TemplateEngine.js',
        'js/AttachmentHandler.js',
        'js/ValidationUtils.js';
        
    StyleSheets = 
        'css/EmailEditor.css',
        'css/Templates.css',
        'css/Responsive.css';
        
    StartupScript = 'js/Startup.js';
    
    // Events from control add-in to AL
    event ControlReady();
    event EmailSaved(EmailData: Text);
    event EmailSent(EmailData: Text);
    event TemplateSelected(TemplateId: Text);
    event AttachmentAdded(AttachmentInfo: Text);
    event AttachmentRemoved(AttachmentId: Text);
    event ValidationError(ErrorMessage: Text);
    
    // Procedures callable from AL
    procedure LoadEmailData(EmailDataJson: Text);
    procedure SetTemplate(TemplateData: Text);
    procedure AddAttachment(AttachmentData: Text);
    procedure RemoveAttachment(AttachmentId: Text);
    procedure SetConfiguration(ConfigData: Text);
    procedure ClearEditor();
    procedure SetReadOnly(ReadOnly: Boolean);
    procedure FocusEditor();
}
```

### Example 6: CSS Configuration

```css
/* EmailEditor.css */
.email-editor-container {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #ffffff;
    border: 1px solid #d1d5db;
    border-radius: 8px;
    padding: 0;
    margin: 0;
    height: 100%;
    overflow: hidden;
}

.editor-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 12px 20px;
    border-bottom: 1px solid #e5e7eb;
}

.editor-toolbar {
    background-color: #f9fafb;
    border-bottom: 1px solid #e5e7eb;
    padding: 8px 16px;
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
}

.toolbar-button {
    background-color: #ffffff;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    padding: 6px 12px;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.2s;
}

.toolbar-button:hover {
    background-color: #f3f4f6;
    border-color: #9ca3af;
}

.toolbar-button:active {
    background-color: #e5e7eb;
    transform: translateY(1px);
}

.toolbar-button.primary {
    background-color: #3b82f6;
    color: white;
    border-color: #2563eb;
}

.toolbar-button.primary:hover {
    background-color: #2563eb;
}

.email-fields {
    padding: 16px 20px;
    background-color: #ffffff;
    border-bottom: 1px solid #e5e7eb;
}

.email-field {
    margin-bottom: 12px;
}

.email-field label {
    display: block;
    font-weight: 600;
    margin-bottom: 4px;
    color: #374151;
}

.email-field input, .email-field select {
    width: 100%;
    padding: 8px 12px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    font-size: 14px;
    box-sizing: border-box;
}

.email-field input:focus, .email-field select:focus {
    outline: none;
    border-color: #3b82f6;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.email-body-container {
    flex: 1;
    padding: 16px 20px;
    overflow-y: auto;
}

.email-body {
    width: 100%;
    min-height: 300px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    padding: 12px;
    font-family: Arial, sans-serif;
    font-size: 14px;
    line-height: 1.5;
    resize: vertical;
}

.attachment-area {
    background-color: #f9fafb;
    border: 2px dashed #d1d5db;
    border-radius: 8px;
    padding: 20px;
    text-align: center;
    margin: 16px 0;
    cursor: pointer;
    transition: all 0.2s;
}

.attachment-area:hover {
    border-color: #3b82f6;
    background-color: #eff6ff;
}

.attachment-list {
    margin-top: 16px;
}

.attachment-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 12px;
    background-color: #ffffff;
    border: 1px solid #e5e7eb;
    border-radius: 4px;
    margin-bottom: 4px;
}

.attachment-item .remove-attachment {
    color: #ef4444;
    cursor: pointer;
    font-weight: bold;
}

.status-bar {
    background-color: #f3f4f6;
    border-top: 1px solid #e5e7eb;
    padding: 8px 20px;
    font-size: 12px;
    color: #6b7280;
}

/* Responsive design */
@media (max-width: 768px) {
    .editor-toolbar {
        flex-direction: column;
    }
    
    .email-fields {
        padding: 12px 16px;
    }
    
    .email-body-container {
        padding: 12px 16px;
    }
}

/* Loading states */
.loading {
    opacity: 0.6;
    cursor: wait;
}

.spinner {
    border: 2px solid #f3f3f3;
    border-top: 2px solid #3b82f6;
    border-radius: 50%;
    width: 16px;
    height: 16px;
    animation: spin 1s linear infinite;
    display: inline-block;
    margin-right: 8px;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* Error states */
.error-message {
    background-color: #fee2e2;
    color: #dc2626;
    padding: 12px;
    border-radius: 4px;
    margin: 8px 0;
    border-left: 4px solid #dc2626;
}

.success-message {
    background-color: #d1fae5;
    color: #065f46;
    padding: 12px;
    border-radius: 4px;
    margin: 8px 0;
    border-left: 4px solid #10b981;
}
```

## Integration Configuration Examples

### Example 7: Q-Team Authenticator Setup

```al
procedure SetupQTeamAuthenticator(): Boolean
var
    QTEAMAuthSetup: Record "Q-Team Authenticator Setup";
    AuthCodeunit: Codeunit "Q-Team App Authenticator";
begin
    // Check if already configured
    if QTEAMAuthSetup.Get() and QTEAMAuthSetup."Is Configured" then
        exit(true);
    
    // Initialize setup record
    if not QTEAMAuthSetup.Get() then begin
        QTEAMAuthSetup.Init();
        QTEAMAuthSetup.Insert();
    end;
    
    // Configure authentication settings
    QTEAMAuthSetup."Server URL" := 'https://api.q-teamsolutions.com';
    QTEAMAuthSetup."API Version" := 'v2.0';
    QTEAMAuthSetup."Timeout (seconds)" := 30;
    QTEAMAuthSetup."Retry Attempts" := 3;
    QTEAMAuthSetup."Enable Logging" := true;
    QTEAMAuthSetup."Is Configured" := true;
    QTEAMAuthSetup.Modify();
    
    // Test the connection
    exit(AuthCodeunit.TestConnection());
end;
```

### Example 8: Async Processing Configuration

```al
procedure ConfigureAsyncProcessing()
var
    JobQueueCategory: Record "Job Queue Category";
    JobQueueEntry: Record "Job Queue Entry";
begin
    // Create job queue category for EIO processing
    if not JobQueueCategory.Get('EIO-PROCESSING') then begin
        JobQueueCategory.Init();
        JobQueueCategory.Code := 'EIO-PROCESSING';
        JobQueueCategory.Description := 'Edit in Outlook Processing';
        JobQueueCategory.Insert();
    end;
    
    // Create recurring job for email cleanup
    JobQueueEntry.Init();
    JobQueueEntry.ID := CreateGuid();
    JobQueueEntry."Object Type to Run" := JobQueueEntry."Object Type to Run"::Codeunit;
    JobQueueEntry."Object ID to Run" := Codeunit::"EIO Cleanup Manager";
    JobQueueEntry."Job Queue Category Code" := 'EIO-PROCESSING';
    JobQueueEntry.Description := 'EIO: Email Cleanup';
    JobQueueEntry."Recurring Job" := true;
    JobQueueEntry."Run on Mondays" := true;
    JobQueueEntry."Run on Tuesdays" := true;
    JobQueueEntry."Run on Wednesdays" := true;
    JobQueueEntry."Run on Thursdays" := true;
    JobQueueEntry."Run on Fridays" := true;
    JobQueueEntry."Starting Time" := 020000T; // 2:00 AM
    JobQueueEntry."Ending Time" := 040000T;   // 4:00 AM
    JobQueueEntry.Insert(true);
end;
```

## Complete Setup Script

### Example 9: Full Configuration Setup

```al
codeunit 50200 "EIO Complete Setup"
{
    procedure RunCompleteSetup(): Boolean
    var
        SetupResults: Dictionary of [Text, Boolean];
        OverallSuccess: Boolean;
    begin
        OverallSuccess := true;
        
        // Step 1: Setup Q-Team Authenticator
        SetupResults.Add('Q-Team Auth', SetupQTeamAuthenticator());
        
        // Step 2: Configure email templates
        SetupResults.Add('Email Templates', SetupDefaultEmailTemplates());
        
        // Step 3: Configure permissions
        SetupResults.Add('Permissions', SetupPermissions());
        
        // Step 4: Configure async processing
        SetupResults.Add('Async Processing', SetupAsyncProcessing());
        
        // Step 5: Configure integration points
        SetupResults.Add('Integrations', SetupIntegrations());
        
        // Step 6: Test configuration
        SetupResults.Add('Configuration Test', TestConfiguration());
        
        // Check overall success
        foreach var Result in SetupResults.Values() do
            OverallSuccess := OverallSuccess and Result;
        
        // Log setup results
        LogSetupResults(SetupResults, OverallSuccess);
        
        if OverallSuccess then
            Message('Edit in Outlook setup completed successfully!')
        else
            Message('Setup completed with some warnings. Please check the setup log.');
        
        exit(OverallSuccess);
    end;
    
    local procedure SetupDefaultEmailTemplates(): Boolean
    var
        Success: Boolean;
    begin
        Success := true;
        
        try
            CreateSalesInvoiceTemplate();
            CreatePurchaseOrderTemplate();
            CreateQuoteTemplate();
            CreateReminderTemplate();
        catch
            Success := false;
        end;
        
        exit(Success);
    end;
    
    local procedure TestConfiguration(): Boolean
    var
        EIOManagement: Codeunit "Q-Team EIO Management";
        TestResult: Boolean;
    begin
        TestResult := true;
        
        // Test Q-Team connection
        if not TestQTeamConnection() then
            TestResult := false;
        
        // Test email functionality
        if not TestEmailFunctionality() then
            TestResult := false;
        
        // Test control add-in
        if not TestControlAddIn() then
            TestResult := false;
        
        exit(TestResult);
    end;
    
    local procedure LogSetupResults(SetupResults: Dictionary of [Text, Boolean]; OverallSuccess: Boolean)
    var
        Keys: List of [Text];
        SetupKey: Text;
        Result: Boolean;
        LogMessage: Text;
    begin
        LogMessage := 'EIO Setup Results:\n';
        LogMessage += '==================\n';
        
        Keys := SetupResults.Keys();
        foreach SetupKey in Keys do begin
            SetupResults.Get(SetupKey, Result);
            LogMessage += SetupKey + ': ';
            if Result then
                LogMessage += 'SUCCESS\n'
            else
                LogMessage += 'FAILED\n';
        end;
        
        LogMessage += '\nOverall Result: ';
        if OverallSuccess then
            LogMessage += 'SUCCESS'
        else
            LogMessage += 'FAILED';
        
        Session.LogMessage('0000EIO', LogMessage, Verbosity::Normal,
                          DataClassification::SystemMetadata,
                          TelemetryScope::ExtensionPublisher);
    end;
}
```

---

**Configuration Checklist:**

- ✅ Q-Team Authenticator configured and tested
- ✅ Email templates created and customized
- ✅ Permission sets assigned to users
- ✅ Control add-in deployed and functional
- ✅ Async processing jobs configured
- ✅ Integration endpoints tested
- ✅ Error handling and logging enabled
- ✅ User training completed

**Next Steps:**
- [Basic Examples](basic-example.md) - Simple implementation patterns
- [Advanced Integrations](advanced-integrations.md) - Complex scenarios
- [Troubleshooting](../troubleshooting/common-errors.md) - Issue resolution