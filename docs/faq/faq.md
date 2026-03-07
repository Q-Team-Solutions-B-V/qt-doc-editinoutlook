# Frequently Asked Questions (FAQ)

This page contains answers to the most frequently asked questions about Q-Team Solutions Edit in Outlook.

## General Questions

### What exactly is Edit in Outlook?
**Q**: I've heard about Edit in Outlook, but what does it do exactly?

**A**: Edit in Outlook is a Microsoft Dynamics 365 Business Central app that enables you to:
- Edit Business Central document emails in Microsoft Outlook before they are sent
- Send emails via your personal Outlook account without adding your email address to Business Central
- Use Business Central email templates with the familiar Outlook interface
- Automatically attach documents as PDF to emails

### How is this different from normal Business Central email sending?
**Q**: What's the difference between regular email and Edit in Outlook?

**A**: 
| Aspect | Regular BC Email | Edit in Outlook |
|--------|------------------|----------------|
| **Sending** | Direct via BC SMTP | Via personal Outlook |
| **Email address** | Must be configured in BC | Uses your own Outlook account |
| **Editing** | Limited editing in BC | Full Outlook editor |
| **Archiving** | Only in BC | In BC + personal Outlook |
| **Platform** | Business Central | Business Central + Outlook |

### Is this an Outlook add-in?
**Q**: Do I need to install a special Outlook add-in?

**A**: **No!** Edit in Outlook works via EML files that open directly in Outlook. No Outlook add-in installation is needed. It works by:
1. BC generates an .eml file with your document and template
2. Your browser downloads the .eml file  
3. You open the file in Outlook (double-click)
4. Outlook opens the email for editing
5. You send via Outlook as usual

## Installation & Setup

### What do I need to use Edit in Outlook?
**Q**: What software and licenses do I need?

**A**: **Requirements**:
- Microsoft Dynamics 365 Business Central (version 27.0+)
- Microsoft Office 365 with Outlook 
- Q-Team App Authenticator (automatically installed)
- Edit in Outlook license from Q-Team Solutions
- Modern browser (Chrome, Edge, Firefox)

### Can I use this with Business Central On-Premise?
**Q**: Does Edit in Outlook work with on-premise BC installations?

**A**: **Yes!** Edit in Outlook supports both:
- **Business Central SaaS** (via AppSource)
- **Business Central On-Premise** (via .app file installation)

The functionality is identical, only the installation method differs.

### Do I need to add my email address to Business Central?
**Q**: Do I still need to configure my email address in BC?

**A**: **No!** This is exactly the big advantage of Edit in Outlook. Your email address does NOT need to be configured in Business Central. The app automatically uses your personal Outlook account when you open the .eml files.

## Usage & Functionality

### Which documents can I send with Edit in Outlook?
**Q**: For which BC documents can I use Edit in Outlook?

**A**: **Supported documents**:
- ✅ Sales Quotes, Orders, Invoices, Credit Memos
- ✅ Purchase Orders, Invoices, Credit Memos  
- ✅ Posted Invoices, Shipments
- ✅ Warehouse Shipment documents
- ⚠️ Service Documents (basic support)
- ❌ Custom reports (not yet supported)

### Can I customize the email templates?
**Q**: Can I create and use my own email templates?

**A**: **Yes!** You can:
- Use and customize standard Business Central email templates
- Create HTML templates with placeholders (e.g. %CUSTOMER_NAME%, %DOCUMENT_NO%)
- Add company-specific branding  
- Set different templates per document type

**Example template**:
```html
<p>Dear %CUSTOMER_NAME%,</p>
<p>Please find attached our %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>
<p>Best regards,<br>%USER_NAME%</p>
```

### Can I add additional attachments?
**Q**: Can I add other files besides the PDF document?

**A**: **Yes!** In Outlook you can:
- Keep the automatic PDF attachment
- Add extra files via Outlook's "Attach" function
- Add files from your computer, OneDrive, or SharePoint
- Insert images directly in the email body

## Technical Questions

### Does this work with all Outlook versions?
**Q**: Which Outlook versions are supported?

**A**: **Supported versions**:
- ✅ **Outlook 365** (recommended) - Full support
- ✅ **Outlook 2021 LTSC** - Full support  
- ✅ **Outlook Web Access** - Via browser download
- ⚠️ **Outlook 2019** - Basic support
- ❌ **Outlook 2016 & older** - Not supported

### Can I use this on Mac/Linux?
**Q**: Does Edit in Outlook work on platforms other than Windows?

**A**: **Platform support**:
- ✅ **Windows** - Native support
- ✅ **macOS** - Via Outlook for Mac
- ⚠️ **Linux** - Via Outlook Web Access  
- ✅ **Mobile** - Limited support via file sharing

### What happens with large files/emails?
**Q**: Are there limits on file size?

**A**: **Limits**:
- **EML file**: Max 25 MB (browser limitation)
- **PDF attachments**: Max 20 MB (recommended)
- **Total email**: Max 30 MB (Outlook/Exchange limitation)
- **Workaround**: For large files, use SharePoint links instead of direct attachments

## Security & Compliance

### Is Edit in Outlook secure?
**Q**: What about the security of this solution?

**A**: **Security measures**:
- ✅ Uses Q-Team App Authenticator for secure license validation
- ✅ Respects all Business Central user rights
- ✅ No O365 tokens stored in Business Central
- ✅ Emails sent via user's own account (audit trail)
- ✅ HTTPS encryption for all communication
- ✅ No sensitive data persistently stored in browser

### What happens to the .eml files?
**Q**: Do the .eml files remain on my computer?

**A**: **File Management**:
- .eml files are downloaded to your Downloads folder
- After sending in Outlook you can safely delete them  
- Business Central keeps no copy of the .eml files
- **Best Practice**: Regular cleanup of Downloads folder for privacy

### Is this GDPR compliant?
**Q**: Does Edit in Outlook meet GDPR requirements?

**A**: **GDPR Considerations**:
- ⚠️ **Manual compliance required** - App provides no automatic GDPR features
- ➡️ **Data minimization** - Train users to include only necessary customer data in emails
- ➡️ **Right to be forgotten** - Manual process for deletion of email copies
- ➡️ **Audit logging** - Combination of BC and Outlook logs required
- **Recommendation**: Implement organization-specific GDPR process

## Troubleshooting

### The "Edit in Outlook" option doesn't appear
**Q**: I don't see the Edit in Outlook button in my email dialog.

**A**: **Possible solutions**:
1. **Check permissions**: Ensure you have the "QTEAM EIO USER" permission set
2. **Verify app installation**: Check if Edit in Outlook is installed in Extension Management
3. **Check setup**: Go to "Edit in Outlook Setup" and ensure "Enable Edit in Outlook" is set to Yes
4. **Browser refresh**: Refresh your browser page and try again
5. **Contact admin**: Have your BC administrator check the setup

### .eml file is not downloaded
**Q**: Nothing happens when I click "Edit in Outlook".

**A**: **Step-by-step solution**:
1. **Check pop-up blocker**: Ensure your browser doesn't block pop-ups for BC
2. **Enable downloads**: Check if downloads are enabled in browser settings
3. **Clear cache**: Clear browser cache and try again
4. **Try different browser**: Test with Chrome, Edge, or Firefox
5. **Check antivirus**: Some antivirus programs block .eml downloads

### Outlook doesn't open .eml file correctly
**Q**: The .eml file opens in wrong app or not at all.

**A**: **File association fix**:
1. **Windows 10/11**:
   - Right-click on .eml file → "Open with" → "Choose another app"  
   - Select "Microsoft Outlook"
   - Check "Always use this app to open .eml files"
2. **Alternative**: Go to Windows Settings → Apps → Default apps → Choose default apps by file type → .eml → Microsoft Outlook

## Licensing & Cost Questions  

### What about the licensing costs?
**Q**: What does Edit in Outlook cost and how does licensing work?

**A**: **License information**:
- **SaaS**: Via Microsoft AppSource - see current pricing
- **On-Premise**: Contact your solution provider for pricing information
- **Included**: 24/7 Online support, updates (SaaS), Q-Team App Authenticator
- **Per user**: License required for each user who uses Edit in Outlook

### Can I test Edit in Outlook first?
**Q**: Is there a trial version available?

**A**: **Trial options**:
- **SaaS**: Many AppSource apps have free trial period - check AppSource listing
- **On-Premise**: Contact Q-Team Solutions for demo/trial possibilities  
- **Demo**: Contact your solution provider for a demonstration
- **Documentation**: Use this comprehensive documentation to evaluate functionality

## Support & Help

### Where can I get help?
**Q**: What if I have problems or questions that aren't answered here?

**A**: **Support options**:
- 📚 **Documentation**: Complete documentation on this site
- 🐛 **Common Errors**: [Troubleshooting page](../troubleshooting/common-errors.md) for common problems
- 🔧 **Advanced Debug**: [Debug guide](../troubleshooting/debugging.md) for technical problems
- 📞 **Support Team**: Contact your solution provider for technical help
- 📧 **Email**: Contact your system administrator
- 📱 **Phone**: +31 030 820 1333

### How do I stay informed about updates?
**Q**: How do I know when new versions or features are available?

**A**: **Update channels**:
- **SaaS**: Automatic updates via AppSource
- **On-Premise**: Email notifications from Q-Team Solutions  
- **Release Notes**: Check with your solution provider for version updates 
- **Newsletter**: Subscribe to Q-Team Solutions newsletter
- **LinkedIn**: Follow your solution provider on LinkedIn for updates

---

**More questions?**  
Contact your solution provider or system administrator for personal assistance.