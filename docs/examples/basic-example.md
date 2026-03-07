# Basic Examples - Edit in Outlook

This document provides basic examples of how to use the Edit in Outlook functionality in Business Central.

## Simple Email Creation and Editing

### Example 1: Creating a Sales Invoice Email

```al
pageextension 50100 "Sales Invoice EIO" extends "Posted Sales Invoice"
{
    actions
    {
        addlast(processing)
        {
            action(EditInOutlook)
            {
                Caption = 'Edit in Outlook';
                Image = Email;
                Promoted = true;
                PromotedCategory = Process;
                
                trigger OnAction()
                var
                    EditInOutlookMgmt: Codeunit "Q-Team EIO Management";
                begin
                    EditInOutlookMgmt.CreateEmailFromSalesInvoice(Rec);
                end;
            }
        }
    }
}
```

### Example 2: Basic Email Template Setup

#### Customer Statement Email Template
```al
procedure SetupCustomerStatementTemplate()
var
    EmailTemplate: Record "Q-Team Email Template";
begin
    EmailTemplate.Init();
    EmailTemplate.Code := 'CUST-STATEMENT';
    EmailTemplate.Description := 'Customer Statement Email';
    EmailTemplate.Subject := 'Monthly Statement - %CUSTOMER_NAME%';
    EmailTemplate.Body := GetCustomerStatementBody();
    EmailTemplate."Attachment Required" := true;
    EmailTemplate.Insert();
end;

local procedure GetCustomerStatementBody(): Text
begin
    exit('Dear %CUSTOMER_NAME%,' + 
         '\n\nPlease find attached your monthly statement.' +
         '\n\nIf you have any questions, please contact us.' +
         '\n\nBest regards,' +
         '\n%COMPANY_NAME%');
end;
```

### Example 3: Simple Control Add-in Implementation

#### HTML Structure
```html
<!DOCTYPE html>
<html>
<head>
    <title>Edit in Outlook - Basic</title>
    <style>
        .email-editor {
            width: 100%;
            height: 400px;
            border: 1px solid #ccc;
            padding: 10px;
            font-family: Arial, sans-serif;
        }
        
        .toolbar {
            margin-bottom: 10px;
            padding: 5px;
            border-bottom: 1px solid #eee;
        }
        
        .button {
            background-color: #0078d4;
            color: white;
            border: none;
            padding: 8px 16px;
            margin-right: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="toolbar">
        <button class="button" onclick="saveEmail()">Save</button>
        <button class="button" onclick="previewEmail()">Preview</button>
    </div>
    
    <div>
        <label>To:</label>
        <input type="email" id="emailTo" style="width: 100%; margin: 5px 0;">
        
        <label>Subject:</label>
        <input type="text" id="emailSubject" style="width: 100%; margin: 5px 0;">
        
        <label>Body:</label>
        <textarea id="emailBody" class="email-editor" placeholder="Enter your email content here..."></textarea>
    </div>
    
    <script src="EmailEditorBasic.js"></script>
</body>
</html>
```

#### JavaScript Functionality
```javascript
// EmailEditorBasic.js
class BasicEmailEditor {
    constructor() {
        this.initializeEditor();
    }
    
    initializeEditor() {
        // Initialize the editor when the control add-in is ready
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('Ready');
        }
    }
    
    loadEmailData(emailData) {
        const data = JSON.parse(emailData);
        
        document.getElementById('emailTo').value = data.to || '';
        document.getElementById('emailSubject').value = data.subject || '';
        document.getElementById('emailBody').value = data.body || '';
    }
    
    saveEmail() {
        const emailData = {
            to: document.getElementById('emailTo').value,
            subject: document.getElementById('emailSubject').value,
            body: document.getElementById('emailBody').value
        };
        
        // Send data back to Business Central
        if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
            Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('SaveEmail', [JSON.stringify(emailData)]);
        }
    }
    
    previewEmail() {
        const emailData = {
            to: document.getElementById('emailTo').value,
            subject: document.getElementById('emailSubject').value,
            body: document.getElementById('emailBody').value
        };
        
        // Open preview window
        const previewWindow = window.open('', '_blank', 'width=600,height=400');
        previewWindow.document.write(this.generatePreviewHTML(emailData));
    }
    
    generatePreviewHTML(emailData) {
        return `
            <html>
                <head><title>Email Preview</title></head>
                <body style="font-family: Arial, sans-serif; padding: 20px;">
                    <h3>Email Preview</h3>
                    <p><strong>To:</strong> ${emailData.to}</p>
                    <p><strong>Subject:</strong> ${emailData.subject}</p>
                    <hr>
                    <div style="white-space: pre-wrap;">${emailData.body}</div>
                </body>
            </html>
        `;
    }
}

// Initialize the editor
const emailEditor = new BasicEmailEditor();

// Global functions accessible from AL
function saveEmail() {
    emailEditor.saveEmail();
}

function previewEmail() {
    emailEditor.previewEmail();
}

function loadEmailData(emailData) {
    emailEditor.loadEmailData(emailData);
}
```

## Customer Communication Examples

### Example 4: Invoice Follow-up Email

```al
procedure SendInvoiceFollowUp(SalesInvoiceHeader: Record "Sales Invoice Header")
var
    Customer: Record Customer;
    EmailTemplate: Record "Q-Team Email Template";
    EmailMessage: Record "Email Message";
    EditInOutlookMgmt: Codeunit "Q-Team EIO Management";
begin
    Customer.Get(SalesInvoiceHeader."Sell-to Customer No.");
    
    // Create email message
    EmailMessage.Init();
    EmailMessage.Id := CreateGuid();
    EmailMessage."To Recipients" := Customer."E-Mail";
    EmailMessage.Subject := StrSubstNo('Follow-up: Invoice %1', SalesInvoiceHeader."No.");
    EmailMessage.Body := GetInvoiceFollowUpBody(SalesInvoiceHeader, Customer);
    EmailMessage.Insert();
    
    // Add invoice as attachment
    AddInvoiceAttachment(EmailMessage, SalesInvoiceHeader);
    
    // Open in Outlook for editing
    EditInOutlookMgmt.EditEmailInOutlook(EmailMessage.Id);
end;

local procedure GetInvoiceFollowUpBody(SalesInvoiceHeader: Record "Sales Invoice Header"; Customer: Record Customer): Text
var
    Body: Text;
begin
    Body := StrSubstNo('Dear %1,', Customer.Name) + '\n\n';
    Body += StrSubstNo('We wanted to follow up on invoice %1 dated %2.', 
                       SalesInvoiceHeader."No.", 
                       Format(SalesInvoiceHeader."Document Date")) + '\n\n';
    Body += 'Please let us know if you have any questions about this invoice.' + '\n\n';
    Body += 'Best regards,' + '\n';
    Body += CompanyName;
    
    exit(Body);
end;
```

### Example 5: Quote Presentation Email

```al
procedure CreateQuoteEmail(SalesHeader: Record "Sales Header")
var
    Customer: Record Customer;
    EmailMessage: Record "Email Message";
    QuoteBody: Text;
begin
    Customer.Get(SalesHeader."Sell-to Customer No.");
    
    // Prepare quote email
    QuoteBody := 'Dear ' + Customer.Name + ',\n\n';
    QuoteBody += 'Thank you for your interest in our products. ';
    QuoteBody += 'Please find attached our quotation for your review.\n\n';
    QuoteBody += GetQuoteDetails(SalesHeader);
    QuoteBody += '\n\nWe look forward to hearing from you.\n\n';
    QuoteBody += 'Best regards,\n' + CompanyName;
    
    // Create email message
    EmailMessage.Init();
    EmailMessage.Id := CreateGuid();
    EmailMessage."To Recipients" := Customer."E-Mail";
    EmailMessage.Subject := StrSubstNo('Quote %1 - %2', SalesHeader."No.", Customer.Name);
    EmailMessage.Body := QuoteBody;
    EmailMessage.Insert();
    
    // Add quote PDF
    AddQuoteAttachment(EmailMessage, SalesHeader);
    
    // Open for editing
    OpenInEditMode(EmailMessage.Id);
end;

local procedure GetQuoteDetails(SalesHeader: Record "Sales Header"): Text
var
    Details: Text;
begin
    Details := 'Quote Details:\n';
    Details += '- Quote No.: ' + SalesHeader."No." + '\n';
    Details += '- Valid Until: ' + Format(SalesHeader."Quote Valid Until Date") + '\n';
    Details += '- Total Amount: ' + Format(SalesHeader."Amount Including VAT") + '\n';
    
    exit(Details);
end;
```

## Document-Based Examples

### Example 6: Purchase Order Confirmation

```al
procedure SendPOConfirmation(PurchaseHeader: Record "Purchase Header")
var
    Vendor: Record Vendor;
    EmailContent: Text;
begin
    Vendor.Get(PurchaseHeader."Buy-from Vendor No.");
    
    EmailContent := BuildPOConfirmationEmail(PurchaseHeader, Vendor);
    
    CreateAndSendEmail(
        Vendor."E-Mail",
        StrSubstNo('PO Confirmation: %1', PurchaseHeader."No."),
        EmailContent,
        PurchaseHeader
    );
end;

local procedure BuildPOConfirmationEmail(PurchaseHeader: Record "Purchase Header"; Vendor: Record Vendor): Text
var
    Body: Text;
    PurchaseLine: Record "Purchase Line";
    LineCount: Integer;
begin
    Body := 'Dear ' + Vendor.Name + ',\n\n';
    Body += 'This email confirms our purchase order as detailed below:\n\n';
    Body += 'PO Number: ' + PurchaseHeader."No." + '\n';
    Body += 'Order Date: ' + Format(PurchaseHeader."Order Date") + '\n';
    Body += 'Expected Receipt Date: ' + Format(PurchaseHeader."Expected Receipt Date") + '\n\n';
    
    // Add line items
    Body += 'Items Ordered:\n';
    PurchaseLine.SetRange("Document No.", PurchaseHeader."No.");
    PurchaseLine.SetRange("Document Type", PurchaseHeader."Document Type");
    
    if PurchaseLine.FindSet() then
        repeat
            LineCount += 1;
            Body += StrSubstNo('- %1: %2 x %3\n', 
                              PurchaseLine.Description,
                              Format(PurchaseLine.Quantity),
                              Format(PurchaseLine."Unit Cost"));
        until PurchaseLine.Next() = 0;
    
    Body += '\nPlease confirm receipt of this order.\n\n';
    Body += 'Thank you,\n' + CompanyName;
    
    exit(Body);
end;
```

### Example 7: Service Request Follow-up

```al
procedure FollowUpServiceRequest(ServiceHeader: Record "Service Header")
var
    Customer: Record Customer;
    ServiceItem: Record "Service Item";
    EmailBody: Text;
begin
    Customer.Get(ServiceHeader."Customer No.");
    
    EmailBody := 'Dear ' + Customer.Name + ',\n\n';
    EmailBody += 'We are following up on your service request:\n\n';
    EmailBody += 'Service Order: ' + ServiceHeader."No." + '\n';
    EmailBody += 'Date: ' + Format(ServiceHeader."Order Date") + '\n';
    
    // Add service items
    EmailBody += GetServiceItemDetails(ServiceHeader);
    
    EmailBody += '\nOur technician will contact you to schedule the service.\n\n';
    EmailBody += 'Best regards,\n' + CompanyName;
    
    CreateEditableEmail(Customer."E-Mail", 'Service Request Follow-up', EmailBody);
end;

local procedure GetServiceItemDetails(ServiceHeader: Record "Service Header"): Text
var
    ServiceItemLine: Record "Service Item Line";
    Details: Text;
begin
    Details := '\nService Items:\n';
    
    ServiceItemLine.SetRange("Document No.", ServiceHeader."No.");
    if ServiceItemLine.FindSet() then
        repeat
            Details += '- ' + ServiceItemLine.Description + '\n';
            if ServiceItemLine."Fault Reason Code" <> '' then
                Details += '  Issue: ' + ServiceItemLine."Fault Reason Code" + '\n';
        until ServiceItemLine.Next() = 0;
    
    exit(Details);
end;
```

---

**Next Steps:**
- [Advanced Integrations](advanced-integrations.md) - Complex scenarios and customizations
- [Sample Configuration](sample-config.md) - Complete setup examples
- [Troubleshooting](../troubleshooting/common-errors.md) - Common issues and solutions