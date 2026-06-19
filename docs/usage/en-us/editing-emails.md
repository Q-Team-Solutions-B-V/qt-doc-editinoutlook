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

## Supported Documents

### Sales Documents
| Document Type | Business Central Page | Available Actions |
|---------------|----------------------|------------------|
| **Sales Quotes** | Sales Quote (41, 42, 43) | Send Email → Edit in Outlook |
| **Sales Orders** | Sales Order (44, 45, 46) | Send Email → Edit in Outlook |
| **Sales Invoices** | Sales Invoice (132, 133, 134) | Send Email → Edit in Outlook |
| **Posted Sales Invoices** | Posted Sales Invoice (132) | Send Email → Edit in Outlook |
| **Sales Credit Memos** | Sales Credit Memo (114, 115) | Send Email → Edit in Outlook |

### Purchase Documents
| Document Type | Business Central Page | Available Actions |
|---------------|----------------------|------------------|
| **Purchase Quotes** | Purchase Quote (49, 50, 51) | Send Email → Edit in Outlook |
| **Purchase Orders** | Purchase Order (52, 53, 54) | Send Email → Edit in Outlook |
| **Purchase Invoices** | Purchase Invoice (122, 123, 124) | Send Email → Edit in Outlook |
| **Purchase Credit Memos** | Purchase Credit Memo (124, 125) | Send Email → Edit in Outlook |

### Warehouse Documents
| Document Type | Business Central Page | Available Actions |
|---------------|----------------------|------------------|
| **Warehouse Shipments** | Warehouse Shipment (7337) | Send Email → Edit in Outlook |
| **Posted Whse. Shipments** | Posted Whse. Shipment (7348) | Send Email → Edit in Outlook |

## User Interface

### Business Central Email Dialog
When you select "Send Email", you see:

![Business Central Send Email dialog](../../assets/Send%20Email.png)

### Edit in Outlook Download Prompt
After clicking "Edit in Outlook":

![Download](../../assets/Download.png)

### Outlook Compose Window
The .eml file opens in Outlook with:

![New Message - Outlook](../../assets/New%20Message%20-%20Outlook.png)

## Email Editing Features

### Text Adjustments
In Outlook you can:
- **Change subject line**
- **Adjust body text**:
  - Add personal note
  - Modify template text
  - Adjust formatting (bold, italic, colors)
  - Add lists
  - Insert links

### Attachment Management
- **View existing attachments** (PDF document)
- **Add extra attachments**:
  - Additional documents
  - Images
  - Specifications
  - Contracts
- **Remove attachments** (if needed)
- **Rename attachments**

### Adjusting Recipients
- **Expand To field** with additional recipients
- **Add Cc recipients**
- **Bcc for hidden copies**
- **Validate addresses** via Outlook address book

### Signature & Formatting
- **Personal signature** is automatically added
- **Company branding** retained from template
- **HTML formatting** fully available
- **Rich text editing** with Outlook's editor

## Advanced Features

### Template Personalization
Customize templates per situation:

```html
<!-- Before sending -->
<p>Dear %CUSTOMER_NAME%,</p>
<p>Please find attached %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- After editing in Outlook -->
<p>Dear John Smith,</p>
<p>Following our conversation today, please find attached
our revised Sales Quote SQ001 with the updated pricing.</p>
```

### Bulk Email Editing
For multiple documents:
1. **Use Edit in Outlook** for first document
2. **Save as template** in Outlook
3. **Apply template** for subsequent documents
4. **Personalize** each message

**See also:** [Supported versions](supported-versions.md) | [Limitations](limitations.md)
