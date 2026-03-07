# Debugging Guide - Edit in Outlook

This guide provides comprehensive debugging techniques and tools for troubleshooting the Edit in Outlook application.

## AL Code Debugging  

### Application Insights Integration

#### Telemetry Setup
```al
procedure LogEIOActivity(ActivityName: Text; AdditionalInfo: Text)
var
    Dimensions: Dictionary of [Text, Text];
begin
    if AdditionalInfo <> '' then
        Dimensions.Add('AdditionalInfo', AdditionalInfo);
    
    Dimensions.Add('UserId', UserId());
    Dimensions.Add('CompanyName', CompanyName);
    Dimensions.Add('AppVersion', GetAppVersion());
    
    Session.LogMessage('0000EIO', ActivityName, Verbosity::Normal, 
                       DataClassification::OrganizationIdentifiableInformation,
                       TelemetryScope::ExtensionPublisher, Dimensions);
end;

local procedure GetAppVersion(): Text
var
    AppInfo: ModuleInfo;
begin
    NavApp.GetCurrentModuleInfo(AppInfo);
    exit(Format(AppInfo.AppVersion));
end;
```

#### Email Processing Tracking
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnBeforeProcessEmail', '', false, false)]
local procedure LogEmailProcessingStart(EmailMessage: Record "Email Message"; var IsHandled: Boolean)
begin
    LogEIOActivity('EmailProcessingStarted', 
                   StrSubstNo('MessageId: %1, Subject: %2', 
                             EmailMessage.Id, 
                             EmailMessage.Subject));
end;

[EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnAfterProcessEmail', '', false, false)]  
local procedure LogEmailProcessingCompleted(Success: Boolean; ErrorMessage: Text)
begin
    if Success then
        LogEIOActivity('EmailProcessingCompleted', 'Success')
    else
        LogEIOActivity('EmailProcessingFailed', 'Error: ' + ErrorMessage);
end;
```

### Debugging Techniques

#### Variable Inspection with Message Dialogs
```al
procedure DebugEmailContent(var EmailMessage: Record "Email Message")
var
    DebugInfo: Text;
    AttachmentCount: Integer;
begin
    // Only in development environments
    if not IsDebuggingEnabled() then
        exit;
        
    AttachmentCount := GetAttachmentCount(EmailMessage);
    
    DebugInfo := 'EMAIL DEBUG INFO:\n';
    DebugInfo += '================\n';
    DebugInfo += 'ID: ' + Format(EmailMessage.Id) + '\n';
    DebugInfo += 'Subject: ' + EmailMessage.Subject + '\n';
    DebugInfo += 'From: ' + EmailMessage."Sender Name" + '\n';
    DebugInfo += 'Body Length: ' + Format(StrLen(EmailMessage.Body)) + '\n';
    DebugInfo += 'Attachments: ' + Format(AttachmentCount) + '\n';
    
    Message('%1', DebugInfo);
end;

local procedure IsDebuggingEnabled(): Boolean
var
    QTEAMSetup: Record "Q-Team EIO Setup";
begin
    if QTEAMSetup.Get() then
        exit(QTEAMSetup."Debug Mode Enabled");
        
    exit(false);
end;
```

#### Using Error Handlers for Complex Debugging
```al
procedure ProcessEmailWithDebug(EmailMessageId: Guid): Boolean
var
    StartTime: DateTime;
    ElapsedTime: Duration;
begin
    StartTime := CurrentDateTime();
    
    if not TryProcessEmail(EmailMessageId) then begin
        ElapsedTime := CurrentDateTime() - StartTime;
        
        Session.LogMessage('0000ERR', 
                          StrSubstNo('Email processing failed after %1ms. Error: %2', ElapsedTime, GetLastErrorText()),
                          Verbosity::Error, 
                          DataClassification::CustomerContent, 
                          TelemetryScope::ExtensionPublisher);
                          
        exit(false);
    end;
    
    ElapsedTime := CurrentDateTime() - StartTime;
    LogEIOActivity('EmailProcessingSuccess', StrSubstNo('Processed in %1ms', ElapsedTime));
    
    exit(true);
end;

[TryFunction]
local procedure TryProcessEmail(EmailMessageId: Guid)
var
    EmailFunctions: Codeunit "Q-Team EIO Email Functions";
begin
    EmailFunctions.ProcessEmailMessage(EmailMessageId);
end;
```

### Session Information

#### Collecting Session Data  
```al
procedure GetSessionInformation(): Text
var
    ActiveSession: Record "Active Session";
    SessionInfo: Text;
begin
    SessionInfo := 'ACTIVE SESSIONS:\n';
    SessionInfo += '================\n';
    
    ActiveSession.SetCurrentKey("User ID");
    ActiveSession.SetRange("User ID", UserId());
    
    if ActiveSession.FindSet() then
        repeat
            SessionInfo += StrSubstNo('Session %1: User %2, Started %3\n',
                                        ActiveSession."Session ID",
                                        ActiveSession."User ID", 
                                        ActiveSession."Login Datetime");
            end;
        until ActiveSession.Next() = 0;
        
    exit(SessionInfo);
end;
```

#### Database Locks Detection
```al
procedure CheckDatabaseLocks()
var
    DatabaseLocks: Query "Database Locks";
    LockInfo: Text;
begin
    LockInfo := 'Current Database Locks:\n';
    
    DatabaseLocks.Open();
    while DatabaseLocks.Read() do begin
        if DatabaseLocks.Object_Name.Contains('EMAIL') or DatabaseLocks.Object_Name.Contains('QTEAM') then begin
            LockInfo += StrSubstNo('Table: %1, Type: %2, User: %3\n',
                                  DatabaseLocks.Object_Name,
                                  DatabaseLocks.Lock_Type,
                                  DatabaseLocks.Login_Name);
        end;
    end;
    DatabaseLocks.Close();
    
    if LockInfo <> 'Current Database Locks:\n' then
        Message('%1', LockInfo);
end;
```

## Control Add-in Debugging

### JavaScript Error Handling

#### Enhanced Error Logging
```javascript
// Global error handler for control add-ins
window.onerror = function(msg, url, lineNo, columnNo, error) {
    const errorInfo = {
        message: msg,
        source: url,
        line: lineNo,
        column: columnNo,
        error: error ? error.stack : 'No stack trace'
    };
    
    console.error('Edit in Outlook JavaScript Error:', errorInfo);
    
    // Send error to Business Central
    if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
        Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('OnJavaScriptError', [JSON.stringify(errorInfo)]);
    }
    
    return false; // Don't suppress default browser error handling
};

// Promise rejection handler
window.addEventListener('unhandledrejection', function(event) {
    console.error('Unhandled Promise Rejection:', event.reason);
    
    if (typeof Microsoft !== 'undefined' && Microsoft.Dynamics && Microsoft.Dynamics.NAV) {
        Microsoft.Dynamics.NAV.InvokeExtensibilityMethod('OnJavaScriptError', 
            [JSON.stringify({type: 'UnhandledPromiseRejection', reason: event.reason})]);
    }
});
```

#### Control Add-in State Debugging
```javascript
class DebugHelper {
    constructor() {
        this.stateHistory = [];
        this.maxHistoryLength = 50;
    }
    
    logState(stateName, stateData) {
        const stateEntry = {
            timestamp: new Date().toISOString(),
            name: stateName,
            data: JSON.parse(JSON.stringify(stateData)) // Deep copy
        };
        
        this.stateHistory.push(stateEntry);
        
        // Maintain history size
        if (this.stateHistory.length > this.maxHistoryLength) {
            this.stateHistory.shift();
        }
        
        console.log('State Change:', stateEntry);
    }
    
    getStateHistory() {
        return this.stateHistory;
    }
    
    exportDebugInfo() {
        const debugInfo = {
            userAgent: navigator.userAgent,
            url: window.location.href,
            timestamp: new Date().toISOString(),
            stateHistory: this.stateHistory,
            performance: performance.timing,
            memory: performance.memory
        };
        
        const blob = new Blob([JSON.stringify(debugInfo, null, 2)], {type: 'application/json'});
        const url = URL.createObjectURL(blob);
        
        const a = document.createElement('a');
        a.href = url;
        a.download = 'edit-in-outlook-debug-' + Date.now() + '.json';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
    }
}

// Global debug helper instance
const debugHelper = new DebugHelper();
```

## Network & Connectivity Debugging

### Connection Testing

#### Business Central API Connectivity
```al
procedure TestBCAPIConnectivity(): Text
var
    HttpClient: HttpClient;
    HttpRequest: HttpRequestMessage;
    HttpResponse: HttpResponseMessage;
    ResponseText: Text;
    Headers: HttpHeaders;
begin
    // Test internal API endpoint
    HttpRequest.SetRequestUri(GetUrl(ClientType::Web) + 'api/v2.0/companies');
    HttpRequest.Method := 'GET';
    
    HttpRequest.GetHeaders(Headers);
    Headers.Add('Authorization', 'Bearer ' + GetBearerToken());
    
    if HttpClient.Send(HttpRequest, HttpResponse) then begin
        HttpResponse.Content.ReadAs(ResponseText);
        exit('API Test Successful: ' + Format(HttpResponse.HttpStatusCode));
    end else
        exit('API Test Failed');
end;
```

#### Q-Team Services Connectivity  
```al
procedure TestQTeamConnectivity(): Text
var
    HttpClient: HttpClient;
    HttpRequest: HttpRequestMessage;  
    HttpResponse: HttpResponseMessage;
    QTeamAuth: Codeunit "Q-Team App Authenticator";
begin
    HttpRequest.SetRequestUri('https://api.q-teamsolutions.com/health');
    HttpRequest.Method := 'GET';
    
    if HttpClient.Send(HttpRequest, HttpResponse) then
        exit('Q-Team API: ' + Format(HttpResponse.HttpStatusCode))
    else
        exit('Q-Team API: Connection Failed');
end;
```

### Firewall & Proxy Issues

#### Connection Diagnostics Script
```powershell
# PowerShell script for network diagnostics
function Test-EIOConnectivity {
    param(
        [string]$BusinessCentralURL,
        [string]$ProxyServer = ""
    )
    
    Write-Host "=== Edit in Outlook Connectivity Test ===" -ForegroundColor Yellow
    
    # Test basic connectivity
    $endpoints = @(
        $BusinessCentralURL,
        "https://api.q-teamsolutions.com",
        "https://login.microsoftonline.com"
    )
    
    foreach ($endpoint in $endpoints) {
        try {
            Write-Host "Testing $endpoint..." -NoNewline
            $response = Invoke-WebRequest -Uri $endpoint -Method Head -TimeoutSec 10
            Write-Host " OK ($($response.StatusCode))" -ForegroundColor Green
        }
        catch {
            Write-Host " FAILED" -ForegroundColor Red  
            Write-Host "  Error: $($_.Exception.Message)" -ForegroundColor Red
        }
    }
    
    # Test DNS resolution
    Write-Host "`nDNS Resolution Test:" -ForegroundColor Yellow
    $dnsNames = @("businesscentral.dynamics.com", "api.q-teamsolutions.com")
    
    foreach ($dns in $dnsNames) {
        try {
            $resolved = Resolve-DnsName -Name $dns -ErrorAction Stop
            Write-Host "$dns -> $($resolved[0].IPAddress)" -ForegroundColor Green
        }
        catch {
            Write-Host "$dns -> FAILED" -ForegroundColor Red
        }
    }
}

# Run the test
Test-EIOConnectivity -BusinessCentralURL "https://your-bc-instance.businesscentral.dynamics.com"
```

## Performance Debugging

### Response Time Analysis

#### Method Performance Tracking
```al
codeunit 50200 "Performance Tracker"
{
    var
        StartTimes: Dictionary of [Text, DateTime];
    
    procedure StartTimer(MethodName: Text)
    begin
        StartTimes.Set(MethodName, CurrentDateTime);
    end;
    
    procedure EndTimer(MethodName: Text): Integer
    var
        StartTime: DateTime;
        Duration: Integer;
    begin
        if StartTimes.Get(MethodName, StartTime) then begin
            Duration := CurrentDateTime - StartTime;
            
            Session.LogMessage('0000PERF', StrSubstNo('Method %1 took %2ms', MethodName, Duration),
                             Verbosity::Verbose, DataClassification::SystemMetadata, 
                             TelemetryScope::ExtensionPublisher);
            
            StartTimes.Remove(MethodName);
            exit(Duration);
        end;
        
        exit(0);
    end;
}
```

#### Usage in EML Generation
```al
[EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnBeforeGenerateEML', '', false, false)]
local procedure StartPerformanceTracking(EmailMessageId: Guid; var IsHandled: Boolean)
var
    PerfTracker: Codeunit "Performance Tracker";
begin
    PerfTracker.StartTimer('EMLGeneration_' + Format(EmailMessageId));
end;

[EventSubscriber(ObjectType::Codeunit, Codeunit::QTEAMEIOEmailFunctions, 'OnAfterGenerateEML', '', false, false)]
local procedure EndPerformanceTracking(FileName: Text; FileContent: InStream)
var
    PerfTracker: Codeunit "Performance Tracker";
    EmailMessageId: Guid;
begin
    // Extract message ID from filename (implement as needed)
    EmailMessageId := ExtractMessageIdFromFileName(FileName);
    
    PerfTracker.EndTimer('EMLGeneration_' + Format(EmailMessageId));
end;
```

## Debug Tools & Utilities

### Debug Information Collector

#### Comprehensive System Info
```al
procedure GenerateDebugReport(): Text
var
    DebugReport: Text;
    AppInfo: ModuleInfo;
    SystemInfo: Text;
begin
    NavApp.GetCurrentModuleInfo(AppInfo);
    
    DebugReport := '=== EDIT IN OUTLOOK DEBUG REPORT ===\n';
    DebugReport += 'Generated: ' + Format(CurrentDateTime) + '\n\n';
    
    // App Information
    DebugReport += '[APP INFORMATION]\n';
    DebugReport += 'App Version: ' + Format(AppInfo.AppVersion) + '\n';
    DebugReport += 'Publisher: ' + AppInfo.Publisher + '\n';
    DebugReport += 'Platform: ' + ApplicationVersion() + '\n\n';
    
    // User Context
    DebugReport += '[USER CONTEXT]\n';
    DebugReport += 'User ID: ' + UserId() + '\n';
    DebugReport += 'Company: ' + CompanyName + '\n';
    DebugReport += 'Session ID: ' + Format(SessionId()) + '\n\n';
    
    // Configuration
    DebugReport += '[CONFIGURATION]\n';
    DebugReport += GetConfigurationInfo() + '\n';
    
    // Permission Check
    DebugReport += '[PERMISSIONS]\n';
    DebugReport += GetPermissionInfo() + '\n';
    
    // Q-Team Status
    DebugReport += '[Q-TEAM AUTHENTICATOR]\n';
    DebugReport += GetAuthenticatorStatus() + '\n';
    
    exit(DebugReport);
end;
```

### Log Export Utility
```al
procedure ExportDebugLogs(FromDate: Date; ToDate: Date)
var
    TempBlob: Codeunit "Temp Blob";
    OutStream: OutStream;
    LogEntries: Text;
begin
    LogEntries := CollectLogEntries(FromDate, ToDate);
    
    TempBlob.CreateOutStream(OutStream, TextEncoding::UTF8);
    OutStream.WriteText(LogEntries);
    
    DownloadFromStream(TempBlob.CreateInStream(), 'EIO-Debug-Logs.txt', '', '', 'debug-logs.txt');
end;
```

---

**Next Steps:**
- [Common Errors](common-errors.md) - Basic troubleshooting
- [FAQ](../faq/faq.md) - Frequently asked debug questions
- [Q-Team Support](https://www.q-teamsolutions.com/support/) - Professional debug assistance