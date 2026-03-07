# Sales Invoice API Documentation

## Overview

This API provides read-only access to posted sales invoices with the ability to retrieve invoice data and PDF attachments from Business Central.

## API Information

- **Version**: 1.0.0
- **Type**: RESTful API
- **Format**: JSON (OData v4)
- **Authentication**: OAuth2
- **License**: Proprietary

## Base URLs

### Production Environment
```
https://{environment}.api.businesscentral.dynamics.com/v2.0/{tenant}/Production/api/yourcompany/editinoutlook/v1.0
```

### Sandbox Environment
```
https://{environment}.api.businesscentral.dynamics.com/v2.0/{tenant}/Sandbox/api/yourcompany/editinoutlook/v1.0
```

**URL Variables:**
- `{environment}`: Business Central environment (api for SaaS, or custom domain for on-premises)
- `{tenant}`: Azure AD tenant ID or domain

## Authentication

### OAuth2 Configuration

The API uses OAuth2 authentication with the following scope:
- **Scope**: `https://api.businesscentral.dynamics.com/Financials.ReadWrite.All`
- **Authorization URL**: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize`  
- **Token URL**: `https://login.microsoftonline.com/common/oauth2/v2.0/token`

### Example Authorization Header
```http
Authorization: Bearer {your-access-token}
```

## Endpoints

### 1. Get Sales Invoices

**GET** `/salesInvoices`

Retrieves a list of posted sales invoices with basic information and Base64 encoded PDF content.

#### Query Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `$select` | string | No | Select specific fields to return | `id,no,billToName,amount,pdfInvoice` |
| `$filter` | string | No | Filter the results | `billToCustomerNo eq '20000'` |
| `$orderby` | string | No | Order the results | `postingDate desc` |
| `$top` | integer | No | Limit number of results (1-20000) | `50` |
| `$skip` | integer | No | Skip a number of results | `0` |

#### Example Request
```http
GET /salesInvoices?$filter=billToCustomerNo eq '20000'&$top=10&$orderby=postingDate desc
Authorization: Bearer {your-access-token}
```

#### Example Response (200 OK)
```json
{
  "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/tenant/Production/api/yourcompany/editinoutlook/v1.0/$metadata#salesInvoices",
  "value": [
    {
      "@odata.etag": "W/\"JzE5OzczNjYzNDM4MjIxNDY2OTcwMTYxOzAwOyc=\"",
      "id": "c44ac32c-80d0-f011-8bcf-6045bdc89f91",
      "billToCustomerNo": "20000",
      "no": "103001",
      "postingDate": "2023-01-17",
      "billToName": "Trey Research",
      "amount": 165.6,
      "amountIncludingVAT": 200.38,
      "pdfInvoice": "JVBERi0xLjcNCiW..."
    }
  ]
}
```

### 2. Get Sales Invoice by ID

**GET** `/salesInvoices({id})`

Retrieves a specific sales invoice by its unique identifier, including the Base64 encoded PDF.

#### Path Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `id` | string (UUID) | Yes | Unique identifier of the sales invoice | `c44ac32c-80d0-f011-8bcf-6045bdc89f91` |

#### Query Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `$select` | string | No | Select specific fields to return | `id,no,billToName,pdfInvoice` |

#### Example Request
```http
GET /salesInvoices(c44ac32c-80d0-f011-8bcf-6045bdc89f91)?$select=id,no,billToName,pdfInvoice
Authorization: Bearer {your-access-token}
```

#### Example Response (200 OK)
```json
{
  "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/tenant/Production/api/yourcompany/editinoutlook/v1.0/$metadata#salesInvoices/$entity",
  "@odata.etag": "W/\"JzE5OzczNjYzNDM4MjIxNDY2OTcwMTYxOzAwOyc=\"",
  "id": "c44ac32c-80d0-f011-8bcf-6045bdc89f91",
  "billToCustomerNo": "20000",
  "no": "103001",
  "postingDate": "2023-01-17",
  "billToName": "Trey Research",
  "amount": 165.6,
  "amountIncludingVAT": 200.38,
  "pdfInvoice": "JVBERi0xLjcNCiW..."
}
```

## Data Models

### Sales Invoice Object

| Field | Type | Description | Example | Max Length |
|-------|------|-------------|---------|------------|
| `@odata.etag` | string | ETag for optimistic concurrency | `W/\"JzE5OzczNjY...\"` | - |
| `id` | string (UUID) | Unique identifier (SystemId) | `c44ac32c-80d0-f011-8bcf-6045bdc89f91` | - |
| `billToCustomerNo` | string | Customer number for billing | `20000` | 20 |
| `no` | string | Invoice number | `103001` | 20 |
| `postingDate` | string (date) | Date when invoice was posted | `2023-01-17` | - |
| `billToName` | string | Name of customer being billed | `Trey Research` | 100 |
| `amount` | number (decimal) | Invoice amount excluding VAT | `165.6` | - |
| `amountIncludingVAT` | number (decimal) | Invoice amount including VAT | `200.38` | - |
| `pdfInvoice` | string (base64) | Base64 encoded PDF content | `JVBERi0xLjcNCiW...` | - |

### PDF Invoice Field

The `pdfInvoice` field contains the complete sales invoice as a Base64 encoded PDF file:

- **Format**: Base64 string
- **Content**: Complete PDF document
- **Usage**: Can be decoded and saved as a PDF file
- **Fallback**: Returns empty string if PDF generation fails

#### Decoding PDF Example (JavaScript)
```javascript
// Convert Base64 to PDF and download
function downloadPDF(base64Data, filename) {
    const byteCharacters = atob(base64Data);
    const byteNumbers = new Array(byteCharacters.length);
    
    for (let i = 0; i < byteCharacters.length; i++) {
        byteNumbers[i] = byteCharacters.charCodeAt(i);
    }
    
    const byteArray = new Uint8Array(byteNumbers);
    const blob = new Blob([byteArray], {type: 'application/pdf'});
    
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.style.display = 'none';
    a.href = url;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    window.URL.revokeObjectURL(url);
}

// Usage
downloadPDF(invoiceData.pdfInvoice, `Invoice-${invoiceData.no}.pdf`);
```

## HTTP Response Codes

| Code | Status | Description |
|------|--------|-------------|
| 200 | OK | Request successful |
| 400 | Bad Request | Invalid query parameters |
| 401 | Unauthorized | Invalid or missing authentication |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Sales invoice not found |
| 500 | Internal Server Error | Server error occurred |

## Error Response Format

All error responses follow this structure:

```json
{
  "error": {
    "code": "BadRequest",
    "message": "Invalid query parameter",
    "details": [
      {
        "code": "InvalidFilter",
        "message": "The filter expression is not valid",
        "target": "$filter"
      }
    ]
  }
}
```

## OData Query Examples

### Basic Filtering
```http
# Get invoices for specific customer
GET /salesInvoices?$filter=billToCustomerNo eq '20000'

# Get invoices from specific date
GET /salesInvoices?$filter=postingDate ge 2023-01-01

# Get invoices with amount greater than 1000
GET /salesInvoices?$filter=amount gt 1000
```

### Sorting and Paging
```http
# Sort by date (newest first), limit to 20 results
GET /salesInvoices?$orderby=postingDate desc&$top=20

# Skip first 50 results (pagination)
GET /salesInvoices?$skip=50&$top=25

# Sort by customer name then by date
GET /salesInvoices?$orderby=billToName,postingDate desc
```

### Field Selection
```http
# Get only essential fields
GET /salesInvoices?$select=id,no,billToName,amount

# Get only PDF without other data
GET /salesInvoices?$select=id,no,pdfInvoice
```

### Combined Queries
```http
# Complex query: Recent invoices for specific customer, sorted by amount
GET /salesInvoices?$filter=billToCustomerNo eq '20000' and postingDate ge 2023-01-01&$orderby=amount desc&$top=10&$select=id,no,postingDate,amount,pdfInvoice
```

## Usage Examples

### Example 1: Get Invoice List for Email Integration
```javascript
async function getInvoicesForEmail(customerNo, limit = 10) {
    const response = await fetch(`/salesInvoices?$filter=billToCustomerNo eq '${customerNo}'&$top=${limit}&$select=id,no,postingDate,billToName,amount,pdfInvoice`, {
        headers: {
            'Authorization': 'Bearer ' + accessToken,
            'Content-Type': 'application/json'
        }
    });
    
    if (response.ok) {
        const data = await response.json();
        return data.value;
    } else {
        throw new Error('Failed to fetch invoices');
    }
}
```

### Example 2: Download Single Invoice PDF
```javascript
async function downloadInvoicePDF(invoiceId) {
    const response = await fetch(`/salesInvoices(${invoiceId})?$select=no,pdfInvoice`, {
        headers: {
            'Authorization': 'Bearer ' + accessToken
        }
    });
    
    if (response.ok) {
        const invoice = await response.json();
        if (invoice.pdfInvoice) {
            downloadPDF(invoice.pdfInvoice, `Invoice-${invoice.no}.pdf`);
        } else {
            console.error('PDF not available for this invoice');
        }
    }
}
```

## Integration Notes

### Performance Considerations
- **PDF Size**: PDF files can be large, consider using `$select` to exclude PDF when not needed
- **Paging**: Use `$top` and `$skip` for large result sets
- **Filtering**: Always filter results to minimize data transfer
- **Caching**: Consider caching frequently accessed invoice data

### Security Notes
- **OAuth Scope**: Requires `Financials.ReadWrite.All` scope
- **Tenant Isolation**: API automatically filters data by tenant
- **User Permissions**: Respects Business Central user permissions
- **HTTPS Only**: All connections must use HTTPS

### Rate Limiting
- Follow Business Central API rate limiting guidelines
- Implement retry logic with exponential backoff
- Monitor API usage through Business Central telemetry

---

## External Resources

- [Business Central API Documentation](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)
- [OData Query Options](https://docs.oasis-open.org/odata/odata/v4.01/odata-v4.01-part2-url-conventions.html)
- [OAuth2 Authentication Guide](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)

---

*For technical support, contact your solution provider or system administrator.*