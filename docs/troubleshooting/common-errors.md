# Common Errors

This page contains an overview of the most common problems when using Edit in Outlook and their solutions.

## Download & Browser Problems

### EML File Not Downloaded

#### Symptoms
- No download prompt appears
- Download starts but stops immediately  
- "Download failed" message in browser
- File is downloaded but is 0 bytes

#### Possible Causes & Solutions

##### Pop-up Blocker
**Cause**: Browser blocks download popup
**Solution**:
1. **Chrome**: 
   - Go to `chrome://settings/content/popups`
   - Add your Business Central URL to "Allowed to show pop-ups"
   - Or click on popup blocker icon right of address bar → "Always allow"

2. **Edge**:
   - Go to `edge://settings/content/popups`  
   - Add Business Central domain to exceptions
   - Check for popup blocker notification in address bar

3. **Firefox**:
   - Go to `about:preferences#privacy`
   - Under "Permissions", click "Settings..." next to "Block pop-up windows"
   - Add Business Central URL as exception

##### Browser Security Settings
**Cause**: Strict security settings block downloads
**Solution**:
```text
Chrome Security Check:
1. Type chrome://settings/security in address bar
2. Ensure "Standard protection" is selected (not "Enhanced")
3. Check "Manage security keys" - no conflicting settings
4. Clear site data: Settings → Privacy → Clear browsing data

Edge Security Check:  
1. Go to edge://settings/privacy
2. Under "Security", select "Balanced" 
3. Check "Manage certificates" for conflicts
4. Reset site permissions if needed
```

### Browser Compatibility Issues

#### Old Browser Version
**Symptoms**: Control add-in doesn't load, JavaScript errors
**Solution**:
```text
Minimum Browser Versions:
- Chrome 90+ (recommended 118+)
- Edge 90+ (recommended 118+) 
- Firefox 88+ (recommended 118+)
- Safari 14+ (macOS only)

Update Script (Windows):
1. Open Command Prompt as Administrator
2. For Chrome: winget upgrade Google.Chrome
3. For Edge: winget upgrade Microsoft.Edge  
4. Restart browser completely
```

## Outlook Integration Problems

### EML File Doesn't Open in Outlook

#### Default App Association Incorrect
**Symptoms**: 
- .eml files open in text editor
- "Choose app" dialog appears every time
- Email opens in wrong application

**Solution Windows 10/11**:
1. **Via Windows Settings**:
   ```text
   1. Open Windows Settings (Win + I)
   2. Go to Apps → Default apps  
   3. Scroll to "Choose default apps by file type"
   4. Search for ".eml"
   5. Click on current app → Select "Microsoft Outlook"
   6. Confirm selection
   ```

2. **Via File Explorer**:
   ```text
   1. Find any .eml file in Downloads
   2. Right click → "Open with" → "Choose another app"
   3. Select "Outlook" from list
   4. Check "Always use this app to open .eml files"
   5. Click OK
   ```

3. **Via Registry (Advanced)**:
   ```registry
   Windows Registry Editor Version 5.00
   
   [HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.eml\UserChoice]
   "ProgId"="Outlook.File.eml.15"
   
   [HKEY_CLASSES_ROOT\.eml]
   @="Outlook.File.eml.15"
   ```

#### Outlook Not Installed/Configured
**Symptoms**: "No app associated" error, Outlook not in app selector
**Solution**:
1. **Verify Outlook Installation**:
   ```powershell
   # PowerShell check
   Get-WmiObject -Query "SELECT * FROM Win32_Product WHERE Name LIKE '%Outlook%'"
   
   # Or check via Apps & Features
   Get-AppxPackage | Where-Object {$_.Name -like "*Outlook*"}
   ```

2. **Repair Office Installation**:
   ```text
   1. Open Control Panel → Programs and Features
   2. Find Microsoft Office in the list
   3. Right click → Change
   4. Select "Quick Repair" → Repair  
   5. If that fails, try "Online Repair"
   6. Restart computer after repair
   ```

### Email Content/Format Problems

#### Template Rendering Issues
**Symptoms**: 
- Email body empty or incorrect formatting
- Attachments missing
- Special characters display incorrectly

**Solution**:
1. **Character Encoding Fix**:
   ```al
   // Check template encoding in BC
   procedure ValidateTemplateEncoding(TemplateText: Text): Text
   var
       TempBlob: Codeunit "Temp Blob";
       InStr: InStream;
       OutStr: OutStream;
   begin
       TempBlob.CreateOutStream(OutStr, TextEncoding::UTF8);
       OutStr.WriteText(TemplateText);
       TempBlob.CreateInStream(InStr, TextEncoding::UTF8);
       exit(InStr.ReadText());
   end;
   ```

2. **Template HTML Validation**:
   ```html
   <!-- Problematic HTML -->
   <div style="position: absolute;"> <!-- Not supported -->
   <script>alert('test');</script>   <!-- Security blocked -->
   
   <!-- Correct HTML -->
   <div style="margin: 10px;">      <!-- Supported -->
   <p><strong>Bold text</strong></p> <!-- Supported -->
   ```

## Business Central Configuration Errors

### Permission/Rights Problems

#### "You do not have permission" Errors
**Symptoms**: User gets access denied when using Edit in Outlook
**Diagnosis & Solution**:
```al
// Check user permissions
procedure DiagnoseUserPermissions(UserId: Code[50])
var
    UserPermissionSet: Record "User Permission Set";
    PermissionSet: Record "Permission Set";
begin
    // Check for required permission sets
    RequiredPermissions := 'QTEAM EIO USER,EMAIL';
    
    UserPermissionSet.SetRange("User ID", UserId);
    if UserPermissionSet.FindSet() then
        repeat
            Message('User has: %1', UserPermissionSet."Permission Set ID");
        until UserPermissionSet.Next() = 0;
        
    // Check specific object permissions
    CheckObjectPermission(UserId, ObjectType::Codeunit, [YOUR_EMAIL_FUNCTIONS_ID]); // EIO Email Functions
end;
```

**Solution Steps**:
1. **Assign Required Permission Sets**:
   ```text
   1. Go to Users in Business Central
   2. Select the user
   3. Go to User Permission Sets  
   4. Add "QTEAM EIO USER" 
   5. Add "EMAIL" (if not already present)
   6. Test access
   ```

2. **Check Company Access** (Multi-company):
   ```al
   procedure CheckCompanyAccess(UserId: Code[50]; CompanyName: Text)
   var  
       UserCompanyAccess: Record "User Company Access";
   begin
       UserCompanyAccess.SetRange("User ID", UserId);
       UserCompanyAccess.SetRange("Company Name", CompanyName);
       
       if UserCompanyAccess.IsEmpty then
           Error('User %1 has no access to company %2', UserId, CompanyName);
   end;
   ```

### Q-Team Authenticator Issues

#### License/Authentication Failures
**Symptoms**:
- "License invalid" message
- "Authentication failed" error  
- Token expiry warnings

**Diagnostic Steps**:
1. **Check Authenticator Status**:
   ```text
   1. Search for "Q-Team App Authenticator Setup"
   2. Open setup page
   3. Check License Status field
   4. Verify Customer No. is correct
   5. Check Token Expiry Date
   ```

2. **Test Connection**:
   ```al
   procedure TestAuthenticator()
   var
       QTeamAuth: Codeunit "Q-Team App Authenticator";
       TestResult: Boolean;
   begin
       TestResult := QTeamAuth.TestConnection();
       if TestResult then
           Message('Authenticator connection successful')
       else
           Error('Authenticator connection failed');
   end;
   ```

**Solution**:
```text  
Common Authenticator Fixes:
1. Verify license key is correct (contact Q-Team if unsure)
2. Check internet connectivity from BC server
3. Verify firewall allows outbound HTTPS to your-api-server.com
4. Clear authenticator cache: Delete all entries in "Q-Team Auth Cache"
5. Restart BC service (On-Premise only)
```

## Control Add-in Errors

### JavaScript/Control Add-in Errors

#### "Control add-in failed to load"
**Symptoms**: White screen, "Unable to load control add-in", JavaScript console errors
**Diagnosis**:
```javascript
// Open browser Developer Tools (F12)
// Check Console tab for errors:
console.error("Failed to load: QTEAMEditInOutlookControlAdd");
console.error("SecurityError: Content Security Policy violation");
console.error("ReferenceError: Microsoft is not defined");
```

**Solution**:
1. **Enable JavaScript**:
   ```text
   Chrome:
   1. Go to chrome://settings/content/javascript
   2. Ensure "Sites can use Javascript" is enabled
   3. Check site-specific settings for Business Central
   
   Edge:
   1. Go to edge://settings/content/javascript  
   2. Enable "Allow (recommended)"
   3. Add Business Central to exceptions if needed
   ```

2. **Clear Browser Cache**:
   ```text
   Complete Cache Clear:
   1. Open Developer Tools (F12)
   2. Right click on refresh icon → "Empty Cache and Hard Reload"  
   3. Or: Settings → Privacy → Clear browsing data → "All time"
   4. Include: Cached images/files, Cookies, Site data
   ```

#### Session/Memory Issues
**Symptoms**: Slow performance, browser becomes unresponsive, "Out of memory" errors
**Solution**:
```javascript
// Monitor memory usage in Developer Tools
// Performance tab → Start recording → Stop after issue occurs

// Temporary fixes:
1. Close other tabs/applications
2. Restart browser completely  
3. Increase virtual memory (Windows):
   - Control Panel → System → Advanced → Performance Settings
   - Advanced → Virtual Memory → Custom size: 4096-8192 MB
```

## Document-Specific Problems

### Document Not Found/Available

#### "Document cannot be processed" Error
**Symptoms**: Specific documents fail to generate EML
**Diagnosis**:
```al
procedure DiagnoseDocumentAccess(DocumentType: Enum "Document Type"; DocumentNo: Code[20])
var
    RecRef: RecordRef;
    Document: Variant;
begin
    case DocumentType of
        DocumentType::Quote:
            begin
                SalesHeader.Get(SalesHeader."Document Type"::Quote, DocumentNo);
                Document := SalesHeader;
            end;
        DocumentType::Order:
            begin
                SalesHeader.Get(SalesHeader."Document Type"::Order, DocumentNo);  
                Document := SalesHeader;
            end;
    end;
    
    RecRef.GetTable(Document);
    if not RecRef.ReadPermission then
        Error('No read permission for %1 %2', DocumentType, DocumentNo);
end;
```

#### Report Layout/Template Issues
**Symptoms**: PDF attachment empty, template not applied correctly
**Solution**:
1. **Check Report Selection**:
   ```text  
   1. Go to "Report Selection - Sales" 
   2. Verify correct report assigned for document type
   3. Check "Email Attachment" usage
   4. Test report directly: Run → Preview
   ```

2. **Validate Email Templates**:
   ```text
   1. Go to "Email Templates"
   2. Test template with sample data
   3. Check HTML syntax/validation
   4. Verify placeholder substitution works
   ```

## Performance & Timeout Issues

### Slow EML Generation/Download

#### Large File Handling
**Symptoms**: Very slow download, timeouts, incomplete files
**Solution**:
1. **Optimize PDF Size**:
   ```al
   // Compress PDF before attachment
   procedure OptimizePDFSize(var TempBlob: Codeunit "Temp Blob")
   var
       PDFOptimizer: Codeunit "PDF Optimizer";
   begin
       PDFOptimizer.CompressPDF(TempBlob, 75); // 75% quality
   end;
   ```

2. **Browser Timeout Adjustment**:
   ```text
   Chrome Flags (for development):
   1. Type chrome://flags/ in address bar
   2. Search for "network-time"  
   3. Adjust timeout settings
   4. Restart browser
   
   Production: Split large documents or use external file sharing
   ```

---

**Next steps:**
- [Debugging](debugging.md) - Advanced troubleshooting techniques
- [FAQ](../faq/faq.md) - Frequently asked questions
- [Support Team](contact-your-support-team) - Professional help