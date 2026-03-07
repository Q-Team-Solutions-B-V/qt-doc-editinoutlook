# Voorbeeld Configuratie

Deze pagina bevat praktische voorbeelden van configuraties, templates en implementaties voor Edit in Outlook.

## Basis Setup Voorbeeld

### Complete Setup Configuratie

#### Edit in Outlook Setup
```al
// Voorbeeld van basis setup configuratie
procedure SetupEditInOutlookBasic()
var
    EIOSetup: Record "QTEAM EIO Setup";
begin
    if not EIOSetup.Get() then begin
        EIOSetup.Init();
        EIOSetup.Insert();
    end;
    
    EIOSetup."Enable Edit in Outlook" := true;
    EIOSetup."Show in Email Dialog" := true;
    EIOSetup."Enable PDF Preview" := true;
    EIOSetup."Max File Size (MB)" := 25;
    EIOSetup."Session Timeout (Min)" := 30;
    EIOSetup."Debug Mode" := false;
    EIOSetup."Enable Telemetry" := true;
    
    EIOSetup.Modify();
    
    Message('Edit in Outlook setup completed successfully.');
end;
```

#### Gebruikersrechten Toewijzing
```al
// Bulk gebruikersrechten toewijzing
procedure AssignEIOPermissions(UserIDFilter: Text)
var
    User: Record User;
    UserPermissionSet: Record "User Permission Set";
begin
    User.SetFilter("User Name", UserIDFilter);
    
    if User.FindSet() then
        repeat
            // Basis EIO rechten
            if not UserPermissionSet.Get(User."User Security ID", 'QTEAM EIO USER') then begin
                UserPermissionSet.Init();
                UserPermissionSet."User Security ID" := User."User Security ID";
                UserPermissionSet."Permission Set ID" := 'QTEAM EIO USER';
                UserPermissionSet.Insert();
            end;
            
            // E-mail rechten (als nog niet aanwezig)
            if not UserPermissionSet.Get(User."User Security ID", 'EMAIL') then begin
                UserPermissionSet.Init();
                UserPermissionSet."User Security ID" := User."User Security ID";
                UserPermissionSet."Permission Set ID" := 'EMAIL';
                UserPermissionSet.Insert();
            end;
            
        until User.Next() = 0;
end;
```

## E-mail Template Voorbeelden

### Sales Quote Template

#### HTML Template
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sales Quote</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        .header {
            border-bottom: 2px solid #007ACC;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .company-logo {
            max-width: 200px;
            height: auto;
        }
        .content {
            margin: 20px 0;
        }
        .highlight {
            background-color: #f0f8ff;
            padding: 10px;
            border-left: 4px solid #007ACC;
            margin: 15px 0;
        }
        .footer {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #ccc;
            font-size: 0.9em;
            color: #666;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
        }
        th, td {
            padding: 8px 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background-color: #f5f5f5;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>%COMPANY_NAME%</h1>
        <p>Professional solutions for your business needs</p>
    </div>
    
    <div class="content">
        <p>Dear %CUSTOMER_NAME%,</p>
        
        <p>Thank you for your interest in our products and services. Please find attached our detailed quote for your requirements.</p>
        
        <div class="highlight">
            <strong>Quote Details:</strong><br>
            Quote Number: <strong>%DOCUMENT_NO%</strong><br>
            Quote Date: <strong>%DOCUMENT_DATE%</strong><br>
            Valid Until: <strong>%VALID_UNTIL_DATE%</strong><br>
            Total Amount: <strong>%AMOUNT% %CURRENCY_CODE%</strong>
        </div>
        
        <h3>What's Next?</h3>
        <ul>
            <li>Review the attached quote document</li>
            <li>Contact us with any questions or modifications</li>
            <li>We'll be happy to schedule a meeting to discuss details</li>
            <li>Quote is valid for 30 days from the date issued</li>
        </ul>
        
        <p>We look forward to working with you and helping your business succeed.</p>
        
        <p>Best regards,<br>
        <strong>%USER_NAME%</strong><br>
        %USER_TITLE%<br>
        %COMPANY_NAME%</p>
    </div>
    
    <div class="footer">
        <p>This quote was generated automatically from Microsoft Dynamics 365 Business Central.<br>
        For questions, please contact us at %COMPANY_EMAIL% or %COMPANY_PHONE%.</p>
    </div>
</body>
</html>
```

### Sales Invoice Template

#### Professionele Invoice Template  
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Invoice Notification</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            line-height: 1.6; 
            margin: 0; 
            padding: 20px; 
            background: #f9f9f9; 
        }
        .container { 
            max-width: 600px; 
            margin: 0 auto; 
            background: white; 
            padding: 30px; 
            border-radius: 10px; 
            box-shadow: 0 2px 10px rgba(0,0,0,0.1); 
        }
        .invoice-header { 
            text-align: center; 
            color: #2c3e50; 
            margin-bottom: 30px; 
        }
        .invoice-details { 
            background: #ecf0f1; 
            padding: 20px; 
            border-radius: 5px; 
            margin: 20px 0; 
        }
        .payment-info { 
            background: #e8f5e8; 
            border: 2px solid #27ae60; 
            padding: 15px; 
            border-radius: 5px; 
            margin: 20px 0; 
        }
        .important { 
            color: #e74c3c; 
            font-weight: bold; 
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="invoice-header">
            <h1>📄 Invoice Notification</h1>
            <h2>%COMPANY_NAME%</h2>
        </div>
        
        <p>Dear %CUSTOMER_NAME%,</p>
        
        <p>We hope this email finds you well. Please find attached your invoice for recent services/products.</p>
        
        <div class="invoice-details">
            <h3>📋 Invoice Details</h3>
            <table width="100%">
                <tr><td><strong>Invoice Number:</strong></td><td>%DOCUMENT_NO%</td></tr>
                <tr><td><strong>Invoice Date:</strong></td><td>%DOCUMENT_DATE%</td></tr>
                <tr><td><strong>Due Date:</strong></td><td class="important">%DUE_DATE%</td></tr>
                <tr><td><strong>Total Amount:</strong></td><td><strong>%AMOUNT% %CURRENCY_CODE%</strong></td></tr>
                <tr><td><strong>Payment Terms:</strong></td><td>%PAYMENT_TERMS%</td></tr>
            </table>
        </div>
        
        <div class="payment-info">
            <h3>💳 Payment Information</h3>
            <p>Please process payment by the due date to avoid late fees.</p>
            <p><strong>Payment Methods Accepted:</strong></p>
            <ul>
                <li>Bank transfer to: %BANK_ACCOUNT%</li>
                <li>Online payment via our portal</li>
                <li>Credit card (contact us for details)</li>
            </ul>
        </div>
        
        <h3>❓ Questions?</h3>
        <p>If you have any questions about this invoice, please don't hesitate to contact us:</p>
        <ul>
            <li>📧 Email: %USER_EMAIL%</li>
            <li>📞 Phone: %USER_PHONE%</li>
            <li>💬 Reply directly to this email</li>
        </ul>
        
        <p>Thank you for your business!</p>
        
        <p>Kind regards,<br>
        <strong>%USER_NAME%</strong><br>
        %DEPARTMENT%<br>
        %COMPANY_NAME%</p>
        
        <hr>
        <p style="font-size: 0.8em; color: #666;">
            This invoice was generated automatically from our Business Central system.
            Please retain this email and the attached PDF for your records.
        </p>
    </div>
</body>
</html>
```

## Custom Integration Voorbeelden

### Event Subscriber Implementaties

#### Custom EML Pre-processing
```al
codeunit 50100 "Custom EIO Processing"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnBeforeGenerateEML', '', false, false)]
    local procedure OnBeforeGenerateEMLCustom(EmailMessageId: Guid; var IsHandled: Boolean)
    var
        EmailMessage: Record "Email Message";
        Customer: Record Customer;
        SalesHeader: Record "Sales Header";
        CustomTemplate: Text;
    begin
        if not EmailMessage.Get(EmailMessageId) then
            exit;
            
        // Custom logic: Use VIP template for VIP customers
        if GetCustomerFromEmailMessage(EmailMessage, Customer) then begin
            if Customer."Customer Category" = Customer."Customer Category"::VIP then begin
                CustomTemplate := GetVIPTemplate(EmailMessage);
                if CustomTemplate <> '' then begin
                    UpdateEmailMessageWithTemplate(EmailMessage, CustomTemplate);
                    // Don't set IsHandled = true, let standard process continue
                end;
            end;
        end;
    end;
    
    local procedure GetCustomerFromEmailMessage(EmailMessage: Record "Email Message"; var Customer: Record Customer): Boolean
    var
        EmailRecipient: Record "Email Recipient";
    begin
        EmailRecipient.SetRange("Email Message Id", EmailMessage.Id);
        if EmailRecipient.FindFirst() then
            if Customer.Get(EmailRecipient."Email Address") then // Simplified logic
                exit(true);
        
        exit(false);
    end;
    
    local procedure GetVIPTemplate(EmailMessage: Record "Email Message"): Text
    var
        EmailTemplate: Record "Email Template";
    begin
        // Load VIP-specific template
        if EmailTemplate.Get('VIP_SALES_TEMPLATE') then
            exit(EmailTemplate."Body Content");
            
        exit('');
    end;
}
```

#### Audit Trail Implementation
```al
codeunit 50101 "EIO Audit Trail"
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnAfterGenerateEML', '', false, false)]
    local procedure LogEMLGeneration(FileName: Text; FileContent: InStream)
    var
        EIOAuditLog: Record "EIO Audit Log";
        FileSize: Integer;
    begin
        FileSize := FileContent.Length;
        
        EIOAuditLog.Init();
        EIOAuditLog."Entry No." := GetNextEntryNo();
        EIOAuditLog."User ID" := UserId();
        EIOAuditLog."Generation Time" := CurrentDateTime;
        EIOAuditLog."File Name" := CopyStr(FileName, 1, MaxStrLen(EIOAuditLog."File Name"));
        EIOAuditLog."File Size" := FileSize;
        EIOAuditLog."Document Type" := ExtractDocumentType(FileName);
        EIOAuditLog."Document No." := ExtractDocumentNo(FileName);
        EIOAuditLog.Insert();
        
        // Send notification for large files
        if FileSize > 10000000 then // 10 MB
            NotifyAdminLargeFile(FileName, FileSize);
    end;
    
    local procedure NotifyAdminLargeFile(FileName: Text; FileSize: Integer)
    var
        NotificationMgt: Codeunit "Notification Management";
    begin
        NotificationMgt.SendNotification('LARGE_EML_FILE', 
                                       StrSubstNo('Large EML file generated: %1 (%2 MB)', 
                                                 FileName, Round(FileSize / 1000000, 1)));
    end;
}
```

### Customer-Specific Templates

#### Template Selection Logic
```al
codeunit 50102 "Dynamic Template Selection"
{
    procedure GetCustomerSpecificTemplate(CustomerNo: Code[20]; DocumentType: Text): Text
    var
        Customer: Record Customer;
        EmailTemplate: Record "Email Template";
        TemplateCode: Code[20];
    begin
        if not Customer.Get(CustomerNo) then
            exit(GetDefaultTemplate(DocumentType));
            
        // Priority 1: Customer-specific template
        TemplateCode := CustomerNo + '_' + DocumentType;
        if EmailTemplate.Get(TemplateCode) then
            exit(EmailTemplate."Body Content");
            
        // Priority 2: Customer category template
        case Customer."Customer Category" of
            Customer."Customer Category"::VIP:
                TemplateCode := 'VIP_' + DocumentType;
            Customer."Customer Category"::Partner:
                TemplateCode := 'PARTNER_' + DocumentType;
            else
                TemplateCode := 'STANDARD_' + DocumentType;
        end;
        
        if EmailTemplate.Get(TemplateCode) then
            exit(EmailTemplate."Body Content");
            
        // Priority 3: Default template
        exit(GetDefaultTemplate(DocumentType));
    end;
    
    procedure GetDefaultTemplate(DocumentType: Text): Text
    var
        EmailTemplate: Record "Email Template";
    begin
        if EmailTemplate.Get('DEFAULT_' + DocumentType) then
            exit(EmailTemplate."Body Content");
            
        // Fallback to system default
        exit(GetSystemDefaultTemplate(DocumentType));
    end;
}
```

## API Integration Voorbeelden

### External System Integration

#### REST API voor EML Generation
```al
api page 50100 "EML Generation API"
{
    APIPublisher = 'YourCompany';
    APIGroup = 'EditInOutlook';
    APIVersion = 'v1.0';
    EntityName = 'emlGeneration';
    EntitySetName = 'emlGenerations';
    SourceTable = "Email Message";
    DelayedInsert = true;
    
    layout
    {
        area(content)
        {
            field(id; Rec.Id) 
            { 
                Caption = 'Message ID';
            }
            field(documentType; DocumentType) 
            { 
                Caption = 'Document Type';
            }
            field(documentNo; DocumentNo) 
            { 
                Caption = 'Document Number';
            }
            field(customerNo; CustomerNo) 
            { 
                Caption = 'Customer Number';
            }
            field(templateCode; TemplateCode) 
            { 
                Caption = 'Template Code';
            }
            field(generateEML; GenerateEML) 
            { 
                Caption = 'Generate EML File';
                trigger OnValidate()
                begin
                    if GenerateEML then
                        ProcessEMLGeneration();
                end;
            }
        }
    }
    
    var
        DocumentType: Text[50];
        DocumentNo: Code[20];
        CustomerNo: Code[20];
        TemplateCode: Code[20];
        GenerateEML: Boolean;
    
    local procedure ProcessEMLGeneration()
    var
        EIOFunctions: Codeunit QTEAMEIOEmailFunctions;
        EmailMessage: Record "Email Message";
    begin
        if EmailMessage.Get(Rec.Id) then
            EIOFunctions.GenerateEMLFile(Rec.Id);
    end;
}
```

#### PowerShell API Client Voorbeeld
```powershell
# PowerShell script voor bulk EML generation
function Invoke-BulkEMLGeneration {
    param(
        [string]$BaseURL,
        [string]$AccessToken,
        [array]$Documents
    )
    
    $headers = @{
        'Authorization' = "Bearer $AccessToken"
        'Content-Type' = 'application/json'
    }
    
    foreach ($doc in $Documents) {
        $body = @{
            documentType = $doc.Type
            documentNo = $doc.Number
            customerNo = $doc.Customer
            templateCode = $doc.Template
            generateEML = $true
        } | ConvertTo-Json
        
        try {
            $response = Invoke-RestMethod -Uri "$BaseURL/api/v1.0/emlGenerations" -Method Post -Headers $headers -Body $body
            Write-Host "Generated EML for $($doc.Type) $($doc.Number): Success" -ForegroundColor Green
        }
        catch {
            Write-Host "Failed to generate EML for $($doc.Type) $($doc.Number): $($_.Exception.Message)" -ForegroundColor Red
        }
    }
}

# Usage example
$documents = @(
    @{ Type = "Quote"; Number = "SQ001"; Customer = "CUST001"; Template = "SALES_QUOTE" },
    @{ Type = "Order"; Number = "SO001"; Customer = "CUST001"; Template = "SALES_ORDER" },
    @{ Type = "Invoice"; Number = "SI001"; Customer = "CUST002"; Template = "SALES_INVOICE" }
)

Invoke-BulkEMLGeneration -BaseURL "https://your-bc-instance.com" -AccessToken "your-token" -Documents $documents
```

## Multi-Company Setup

### Cross-Company Configuration
```al
codeunit 50103 "Multi-Company EIO Setup"
{
    procedure ConfigureAllCompanies()
    var
        Company: Record Company;
    begin
        Company.SetRange(Blocked, false);
        if Company.FindSet() then
            repeat
                ConfigureCompany(Company.Name);
            until Company.Next() = 0;
    end;
    
    local procedure ConfigureCompany(CompanyName: Text[30])
    var
        EIOSetup: Record "QTEAM EIO Setup";
    begin
        ChangeCompany(CompanyName);
        
        if not EIOSetup.Get() then begin
            EIOSetup.Init();
            EIOSetup.Insert();
        end;
        
        // Standard configuration for all companies
        EIOSetup."Enable Edit in Outlook" := true;
        EIOSetup."Show in Email Dialog" := true;
        EIOSetup."Enable PDF Preview" := true;
        EIOSetup."Max File Size (MB)" := 25;
        EIOSetup.Modify();
        
        // Company-specific templates
        SetupCompanyTemplates(CompanyName);
        
        Message('Setup completed for company: %1', CompanyName);
    end;
    
    local procedure SetupCompanyTemplates(CompanyName: Text[30])
    var
        EmailTemplate: Record "Email Template";
        CompanyInfo: Record "Company Information";
    begin
        CompanyInfo.Get();
        
        // Create company-specific quote template
        CreateTemplateIfNotExists('SALES_QUOTE', 'Sales Quote Template', 
                                 GetQuoteTemplate(CompanyInfo.Name, CompanyInfo."Phone No."));
        
        // Create company-specific invoice template  
        CreateTemplateIfNotExists('SALES_INVOICE', 'Sales Invoice Template',
                                 GetInvoiceTemplate(CompanyInfo.Name, CompanyInfo."Bank Account No."));
    end;
}
```

## Monitoring & Reporting

### Usage Analytics
```al
codeunit 50104 "EIO Analytics"
{
    procedure GenerateUsageReport(FromDate: Date; ToDate: Date): Text
    var
        EIOAuditLog: Record "EIO Audit Log";
        ReportText: Text;
    begin
        ReportText := 'Edit in Outlook Usage Report\n';
        ReportText += '=================================\n';
        ReportText += StrSubstNo('Period: %1 to %2\n\n', FromDate, ToDate);
        
        EIOAuditLog.SetRange("Generation Time", CreateDateTime(FromDate, 0T), CreateDateTime(ToDate, 235959T));
        
        // Total usage
        ReportText += StrSubstNo('Total EML files generated: %1\n', EIOAuditLog.Count());
        
        // By user
        ReportText += '\nTop Users:\n';
        ReportText += GetTopUsers(EIOAuditLog);
        
        // By document type
        ReportText += '\nDocument Types:\n';
        ReportText += GetDocumentTypeStats(EIOAuditLog);
        
        // File size statistics
        ReportText += '\nFile Size Statistics:\n';
        ReportText += GetFileSizeStats(EIOAuditLog);
        
        exit(ReportText);
    end;
    
    local procedure GetTopUsers(var EIOAuditLog: Record "EIO Audit Log"): Text
    var
        TempUser: Record User temporary;
        UserStats: Text;
    begin
        // Implementation for user statistics
        exit(UserStats);
    end;
}
```

---

**Volgende stappen:**
- [Installatie](../installation/installation-overview.md) - Begin met setup
- [API Documentatie](../integration/api-overview.md) - Technische integratie  
- [FAQ](../faq/faq.md) - Veelgestelde vragen