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
/* Problematic CSS */
.unsupported {
    position: absolute;  /* Not widely supported */
    transform: rotate(); /* Email client issues */
    /* @media queries — Limited support */
}
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
A user needs at minimum:
- **Document Read**: For document access
- **Email Template Read**: For template access
- **File Download**: For EML files
- **Control Add-in Execute**: For browser functionality

**See also:** [Editing emails](editing-emails.md) | [Supported versions](supported-versions.md)
