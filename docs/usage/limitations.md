# Limitations

This page describes the known limitations, restrictions and considerations when using Edit in Outlook.

## Technical Limitations

### Browser & Download Limitations

#### File Size Limits
| Component | Maximum Size | Reason | Workaround |
|-----------|-------------|--------|------------|
| **EML File** | 25 MB | Browser download limit | Split large attachments |
| **PDF Attachments** | 20 MB | Email client limits | Compress PDF |
| **Total Email** | 30 MB | Outlook/Exchange limit | Use SharePoint links |
| **Control Add-in** | 100 MB memory | Browser performance | Refresh page |

#### Browser Specific Issues
- **Chrome**: Pop-up blocker may block downloads
- **Firefox**: Encoding issues with non-ASCII characters
- **Edge**: Occasional timeout with large files  
- **Safari**: Limited PDF preview support

### Business Central Platform Limitations

#### SaaS vs On-Premise
| Functionality | SaaS | On-Premise | Note |
|---------------|------|------------|------|
| **Automatic Updates** | ✅ | ❌ | SaaS automatic, On-Prem manual |
| **Custom Extensions** | ⚠️ Limited | ✅ Full | SaaS sandbox restrictions |
| **Debug Mode** | ❌ | ✅ | SaaS security policy |
| **Log Access** | ⚠️ Application Insights | ✅ Direct | Different logging approaches |

#### API Limits
- **Requests per minute**: 100 (SaaS), Unlimited (On-Prem)
- **Session timeout**: 30 minutes default
- **Concurrent users**: Based on license model

## Outlook & Office Limitations

### Outlook Desktop vs Web

#### Feature Comparison
| Feature | Desktop | Web | Mobile |
|---------|---------|-----|--------|
| **EML Opening** | ✅ Native | ⚠️ Via browser | ❌ Limited |
| **Rich Formatting** | ✅ Full | ✅ Full | ⚠️ Basic |
| **Attachment Handling** | ✅ Full | ✅ Full | ⚠️ Upload only |
| **Offline Access** | ✅ Full | ❌ None | ⚠️ Limited |

#### Version Dependencies
- **Outlook 2016/2019**: Limited EML support
- **OWA Legacy**: No direct EML opening
- **Mobile Apps**: Requires desktop preparation step

### Exchange & O365 Limits

#### Email Size Limits
| Platform | Max Message Size | Max Attachments | Max Recipients |
|----------|-----------------|----------------|----------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (default) | Unlimited | 5000 |
| **Exchange 2016** | 25 MB (default) | Unlimited | 5000 |

> **Note**: Organization settings may further restrict these limits

## Document Type Limitations

### Supported vs Unsupported

#### Fully Supported
- ✅ Sales Quotes, Orders, Invoices
- ✅ Purchase Orders, Invoices  
- ✅ Posted Documents
- ✅ Credit Memos
- ✅ Warehouse Shipments

#### Limited Support
- ⚠️ **Service Documents**: Basic template support
- ⚠️ **Job Documents**: Minimal personalization
- ⚠️ **Assembly Orders**: No specific templates

#### Not Supported
- ❌ **Custom Report Objects**: No EML generation
- ❌ **Dataverse Integration**: Only BC native
- ❌ **External Documents**: No third-party support

### Template Limitations

#### HTML Template Issues
```html
<!-- Problematic CSS -->
<style>
    .unsupported { 
        position: absolute;  /* Not widely supported */
        transform: rotate(); /* Email client issues */
        @media queries;      /* Limited support */
    }
</style>
```

#### Supported HTML Subset
- ✅ Basic HTML tags (p, div, table, br)
- ✅ CSS styling (inline preferred)
- ✅ Images (embedded or linked)
- ❌ JavaScript (security blocked)
- ❌ Complex CSS layouts (flexbox, grid)
- ❌ External font loading

## User & Rights Limitations

### Permission Dependencies

#### Minimum Required Rights
A user needs minimum:
- **Document Read**: For document access
- **Email Template Read**: For template access
- **File Download**: For EML files
- **Control Add-in Execute**: For browser functionality

#### Advanced Features
For advanced features:
- **Template Modify**: For custom templates
- **Debug Access**: For troubleshooting
- **Setup Modify**: For configuration changes

### Multi-Company Limitations
- **Cross-company**: Templates are company-specific
- **Shared Resources**: Limited sharing between companies
- **User Context**: Switch between companies requires logout/login

## Performance & Scalability

### Known Performance Issues

#### Large Document Handling
| Document Size | Template Complexity | Expected Load Time |
|---------------|-------------------|------------------|
| < 1 MB | Simple | < 3 seconds |
| 1-5 MB | Medium | 5-10 seconds |
| 5-15 MB | Complex | 15-30 seconds |
| > 15 MB | Any | > 30 seconds (timeout risk) |

#### Concurrent User Limits
- **Recommended**: < 50 concurrent users
- **Performance degradation**: > 100 users
- **System limits**: Depends on BC server resources

### Memory Consumption
| Component | Typical Usage | Peak Usage |
|-----------|--------------|------------|
| **Browser Tab** | 50-100 MB | 200-300 MB |
| **Control Add-in** | 10-30 MB | 50-100 MB |
| **Temp Files** | 5-50 MB | 100-200 MB |

## Security & Compliance Limitations

### Data Protection Issues

#### Temporary File Storage
- **Local Downloads**: EML files in browser downloads
- **Auto Cleanup**: No automatic removal
- **Sensitive Data**: Potentially sensitive info in temp files

#### Audit Trail Gaps
- **Outlook Sending**: Not logged in Business Central
- **Email Modifications**: Changes not tracked
- **Recipient Verification**: No automatic validation

### Compliance Considerations

#### GDPR Compliance
| Aspect | Status | Action Required |  
|--------|--------|-----------------|
| **Data Minimization** | ⚠️ Manual | User training required |
| **Right to be Forgotten** | ❌ Limited | Manual cleanup process |
| **Audit Logging** | ⚠️ Partial | Additional logging needed |
| **Consent Management** | ❌ Not Built-in | External solution needed |

#### Industry Specific
- **Healthcare (HIPAA)**: No specific compliance features
- **Financial (SOX)**: Limited audit trail
- **Government**: No certified security levels

## Integration Limitations

### Third-party Systems

#### CRM Integration  
- **Dynamics 365 Sales**: No direct integration
- **Salesforce**: No built-in connectors
- **Custom CRM**: Requires custom development

#### Document Management
- **SharePoint**: Limited document sharing
- **OneDrive**: No automatic sync
- **Document Templates**: Only BC native templates

### API Limitations

#### External API Access
```al
// Not available in Edit in Outlook:
// - External web service calls
// - Real-time data updates  
// - Cross-company data access
// - Non-BC authentication
```

#### Extension Points
- **Limited Integration Events**: Only core workflow
- **No Custom UI**: Control Add-in not extensible
- **Template Engine**: No third-party template engines

## Workarounds & Mitigations

### Common Workarounds

#### For Large Files
1. **Compress PDF**: Use PDF compression tools
2. **External Links**: Link to SharePoint/OneDrive  
3. **Separate Emails**: Split documentation across multiple emails
4. **ZIP Attachments**: Compress multiple files

#### For Template Issues
1. **Simplified HTML**: Use basic HTML formatting
2. **Inline CSS**: Avoid external stylesheets
3. **Test Templates**: Test in multiple email clients
4. **Fallback Text**: Provide plain text alternative

#### For Browser Issues
1. **Multiple Browsers**: Test different browsers
2. **Incognito Mode**: Test without extensions
3. **Clear Cache**: Regular browser maintenance
4. **Update Browsers**: Maintain current versions

---

**Next steps:**
- [Troubleshooting](../troubleshooting/common-errors.md) - Problem solving
- [FAQ](../faq/faq.md) - Frequently asked questions about limitations
- [API Overview](../integration/api-overview.md) - Extensibility options