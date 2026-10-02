# Q-Team Solutions Edit in Outlook - Extensibility Guide

This guide shows how to create a separate Business Central extension that adds **Edit in Outlook** to a page where it is not available by default.

For this example, we will add the action to the **Customer Card**.

The custom extension uses the public functionality provided by the **Edit In Outlook** app, so no changes to the Edit In Outlook app itself are required.

## 1. Create a new AL project

Open Visual Studio Code and run:

```text
AL: Go!
```

Choose a name for your extension, for example:

```text
EiO-extender
```

When asked for the runtime version, select:

```text
17.0
```

Runtime `17.0` is used for Business Central 28.

Next, choose the environment you want to develop against:

* **Microsoft cloud sandbox** for Business Central SaaS.
* **Your own server** for an On-Premise or locally hosted environment.

## 2. Add the Edit In Outlook dependency

Open the generated `app.json` file and add **Edit In Outlook** as a dependency:

```json
"dependencies": [
    {
        "id": "0e9ac084-9f49-46d3-b3d1-224b4e7dba0a",
        "name": "Edit In Outlook",
        "publisher": "Q-Team Solutions",
        "version": "28.0.46296.0"
    }
]
```

This gives your extension access to the public objects and procedures exposed by Edit In Outlook.

Make sure the object ID range is available for your own extension. Do not reuse the object range of the Edit In Outlook app.

## 3. Configure `launch.json`

Next, configure `.vscode/launch.json` so the project connects to the Business Central environment where Edit In Outlook is installed.

For a cloud sandbox, for example:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "al",
            "name": "Development",
            "request": "launch",
            "environmentType": "Sandbox",
            "environmentName": "Dev",
            "startupObjectId": 21,
            "startupObjectType": "Page",
            "breakOnError": true,
            "launchBrowser": true
        }
    ]
}
```

Page `21` is the standard **Customer Card**, so it will open automatically after publishing.

Change the environment settings where needed to match your own Business Central environment.

## 4. Download symbols

Once `app.json` and `launch.json` are configured, run:

```text
AL: Download Symbols
```

The `.alpackages` folder should now contain the required Microsoft packages and the symbols for Edit In Outlook.

Before continuing, make sure there are no missing-package errors in the project.

## 5. Create the Customer Card extension

Create a new AL file, for example:

```text
src/CustomerCardExt.PageExt.al
```

Before connecting anything to Edit In Outlook, first check that your extension can successfully add an action to the Customer Card.

```al
pageextension 50200 "EiO Customer Card Ext." extends "Customer Card"
{
    actions
    {
        addlast(Processing)
        {
            action(EiOEditInOutlook)
            {
                ApplicationArea = All;
                Caption = 'Test action';
                Image = Email;
                ToolTip = 'This action tests the extensibility of Customer Card.';

                trigger OnAction()
                begin
                    Message(
                        'Extension works for customer %1.',
                        Rec."No.");
                end;
            }
        }
    }
}
```

Publish the extension with `F5`.

Open a Customer Card and look for the **Test action** under the **Actions** menu.

When you select it, Business Central should show the test message.

If that works, you have confirmed that your custom app can successfully extend the Customer Card.

## 6. Connect the action to Edit In Outlook

Now replace the test action with the actual Edit In Outlook implementation.

For the Customer Card, the extension first creates a standard Business Central `Email Message`. The ID of that message is then passed to Edit In Outlook.

```al
pageextension 50200 "EiO Customer Card Ext." extends "Customer Card"
{
    actions
    {
        addlast(Processing)
        {
            action(QTEAMEditInOutlook)
            {
                ApplicationArea = All;
                Caption = 'Edit in Outlook';
                Image = Email;
                ToolTip = 'Create an email for this customer and download it for editing in Outlook.';

                trigger OnAction()
                var
                    EmailMessage: Codeunit "Email Message";
                    QTeamEmailFunctions: Codeunit "QTEAM EIO Email Functions";
                    Subject: Text;
                    Body: Text;
                    NoEmailErr: Label 'Customer %1 does not have an email address.';
                    SubjectLbl: Label 'Customer %1 - %2';
                begin
                    if Rec."E-Mail" = '' then
                        Error(NoEmailErr, Rec."No.");

                    Subject := StrSubstNo(
                        SubjectLbl,
                        Rec."No.",
                        Rec.Name);

                    Body := '';

                    EmailMessage.Create(
                        Rec."E-Mail",
                        Subject,
                        Body,
                        true);

                    QTeamEmailFunctions.EditInOutlook(
                        EmailMessage.GetId());
                end;
            }
        }

        addlast(Promoted)
        {
            actionref(QTEAMEditInOutlookPromoted; QTEAMEditInOutlook)
            {
            }
        }
    }
}
```

The `actionref` also places the action in the main action bar, so users do not have to open the **Actions** menu first.

## 7. How the integration works

The example uses two pieces of functionality:

1. The standard Business Central `Email Message` codeunit creates the email.
2. `QTEAM EIO Email Functions.EditInOutlook(EmailMessageId)` turns that email into an `.eml` file that can be opened in Outlook.

The flow looks like this:

```text
Customer Card
    ↓
Custom page action
    ↓
EmailMessage.Create(...)
    ↓
EmailMessage.GetId()
    ↓
QTEAM EIO Email Functions.EditInOutlook(...)
    ↓
.eml file
    ↓
Microsoft Outlook
```

This allows you to add Edit In Outlook to pages that are not supported by the standard app.

> **Note:** `EditInOutlook()` performs the Edit In Outlook license check itself. If no valid Essential/Premium license or Authenticator key is available, no `.eml` file is generated. If a user interface is available, Edit In Outlook also shows the corresponding license message. You do not need to add a separate license check to your own extension.

## 8. Adapting the example

The same approach can be used on other pages.

Your extension is responsible for deciding what should go into the email, such as:

* the recipient;
* the subject;
* the body;
* any other information you want to include.

In the Customer Card example, the customer's email address is used:

```al
Rec."E-Mail"
```

On another page, simply retrieve the appropriate email address from the related record.

Once the `Email Message` has been prepared, pass its ID to Edit In Outlook:

```al
QTeamEmailFunctions.EditInOutlook(
    EmailMessage.GetId());
```

## 9. Optional: Add an email body

The integration is already complete at this point.

In the previous example, however, the email body is empty:

```al
Body := '';

EmailMessage.Create(
    Rec."E-Mail",
    Subject,
    Body,
    true);
```

`EditInOutlook(EmailMessageId)` does not create a body for you. It uses the body that is already present in the `Email Message`.

So if an empty email is fine for your scenario, you can stop here.

If you want to include a predefined email body, there are two common options.

### 9.1 Option 1: Add the body directly in AL

The simplest approach is to define the email body in your extension.

Replace:

```al
Body := '';
```

with your own HTML, for example:

```al
Body :=
    '<p>Dear ' + Rec.Name + ',</p>' +
    '<p>This email was created from the Customer Card.</p>' +
    '<p>Kind regards,</p>';
```

The relevant part of the action then becomes:

```al
Subject := StrSubstNo(
    SubjectLbl,
    Rec."No.",
    Rec.Name);

Body :=
    '<p>Dear ' + Rec.Name + ',</p>' +
    '<p>This email was created from the Customer Card.</p>' +
    '<p>Kind regards,</p>';

EmailMessage.Create(
    Rec."E-Mail",
    Subject,
    Body,
    true);

QTeamEmailFunctions.EditInOutlook(
    EmailMessage.GetId());
```

The final `true` passed to `EmailMessage.Create()` tells Business Central that the body contains HTML.

The flow is now:

```text
Customer Card
    ↓
Create recipient, subject and body
    ↓
EmailMessage.Create(...)
    ↓
EmailMessage.GetId()
    ↓
EditInOutlook(...)
    ↓
.eml file with email body
    ↓
Microsoft Outlook
```

This option is a good fit when:

* the body can be defined directly in code;
* users do not need to maintain the template in Business Central;
* the page only needs a relatively simple email.

A complete example looks like this:

```al
pageextension 50200 "EiO Customer Card Ext." extends "Customer Card"
{
    actions
    {
        addlast(Processing)
        {
            action(QTEAMEditInOutlook)
            {
                ApplicationArea = All;
                Caption = 'Edit in Outlook';
                Image = Email;
                ToolTip = 'Create an email for this customer and download it for editing in Outlook.';

                trigger OnAction()
                var
                    EmailMessage: Codeunit "Email Message";
                    QTeamEmailFunctions: Codeunit "QTEAM EIO Email Functions";
                    Subject: Text;
                    Body: Text;
                    NoEmailErr: Label 'Customer %1 does not have an email address.';
                    SubjectLbl: Label 'Customer %1 - %2';
                begin
                    if Rec."E-Mail" = '' then
                        Error(NoEmailErr, Rec."No.");

                    Subject := StrSubstNo(
                        SubjectLbl,
                        Rec."No.",
                        Rec.Name);

                    Body :=
                        '<p>Dear ' + Rec.Name + ',</p>' +
                        '<p>This email was created using your Edit in Outlook extension.</p>' +
                        '<p>Kind regards,</p>';

                    EmailMessage.Create(
                        Rec."E-Mail",
                        Subject,
                        Body,
                        true);

                    QTeamEmailFunctions.EditInOutlook(
                        EmailMessage.GetId());
                end;
            }
        }

        addlast(Promoted)
        {
            actionref(QTEAMEditInOutlookPromoted; QTEAMEditInOutlook)
            {
            }
        }
    }
}
```

### 9.2 Option 2: Use a Business Central email body layout

For document pages such as Sales Orders, you can let Business Central generate the body from its existing **Report Selections** and email body layouts.

For example:

```al
QTeamEmailFunctions.EditInOutlook(
    SalesHeader,
    Enum::"Report Selection Usage"::"S.Order",
    Subject,
    CustomerEmail);
```

The important part here is:

```al
Enum::"Report Selection Usage"::"S.Order"
```

This tells Edit In Outlook to use the Report Selections configured for Sales Orders.

From that setup, Edit In Outlook looks for:

* the report marked **Use for Email Attachment**, which is used to create the PDF;
* the report marked **Use for Email Body**, together with its email body layout.

The flow is:

```text
Sales Order
    ↓
Report Selection Usage::S.Order
    ↓
Report Selections
    ├─ PDF attachment
    └─ Email body layout
    ↓
Edit in Outlook
    ↓
.eml file with body and attachment
```

Here is a complete Sales Order example.

For the sake of clarity within our examples, the action is called **Edit in Outlook Ext** so it can easily be distinguished from the standard Edit In Outlook action that may already be available on the page.

```al
pageextension 50201 "EiO Sales Order Ext." extends "Sales Order"
{
    actions
    {
        addlast(Processing)
        {
            action(QTEAMEditInOutlook)
            {
                ApplicationArea = All;
                Caption = 'Edit in Outlook Ext';
                Image = Email;
                ToolTip = 'Create the Sales Order email and download it for editing in Outlook.';

                trigger OnAction()
                var
                    SalesHeader: Record "Sales Header";
                    QTeamEmailFunctions: Codeunit "QTEAM EIO Email Functions";
                    SubjectLbl: Label '%1 %2', Comment = '%1 = Page Caption, %2 = Sales Order No.';
                begin
                    SalesHeader := Rec;
                    SalesHeader.SetRecFilter();

                    QTeamEmailFunctions.EditInOutlook(
                        SalesHeader,
                        Enum::"Report Selection Usage"::"S.Order",
                        StrSubstNo(SubjectLbl, CurrPage.Caption, Rec."No."),
                        GetCustomerEmail());
                end;
            }
        }

        addlast(Promoted)
        {
            actionref(QTEAMEditInOutlookPromoted; QTEAMEditInOutlook)
            {
            }
        }
    }

    local procedure GetCustomerEmail(): Text
    var
        Customer: Record Customer;
        NoEmailErr: Label 'Customer %1 does not have an email address.';
    begin
        if not Customer.Get(Rec."Sell-to Customer No.") then
            exit('');

        if Customer."E-Mail" = '' then
            Error(NoEmailErr, Customer."No.");

        exit(Customer."E-Mail");
    end;
}
```

### 9.3 Using layouts on a page such as Customer Card

The Customer Card is a little different.

Sales Orders already have a standard report selection usage:

```al
Enum::"Report Selection Usage"::"S.Order"
```

There is no equivalent standard value for `Customer`.

So if you want Customer emails to use configurable Business Central layouts, you first need to add your own report selection usage.

For example:

```al
enumextension 50201 "EiO Report Usage Ext." extends "Report Selection Usage"
{
    value(50200; "Customer")
    {
        Caption = 'Customer';
    }
}
```

After that, you still need to:

1. Choose or create a report that works with the Customer record.
2. Configure that report in Report Selections.
3. Set up the email body layout.
4. Use the new `Customer` report selection usage when calling Edit In Outlook.

Once that setup is in place, the custom `Customer` value can be used in the same way as `"S.Order"` in the Sales Order example.

This is a more advanced scenario, so it is not required if you only want to add a simple Edit In Outlook action to the Customer Card.

### 9.4 Which option should you use?

For most simple custom-page integrations, **Option 1** is enough.

Use **Option 2** when you want users to manage the email body through Business Central report selections and layouts, as they do for Sales Orders and Sales Invoices.

If you do not need a predefined email body at all, you can simply use the basic integration from section 6.

**Next steps:**
- [API overview](api-overview.md) - Full list of integration events and extensibility points
- [Authentication](authentication.md) - How licensing and the Authenticator key are checked