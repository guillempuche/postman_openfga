# OpenFGA API Collection

A Postman collection for interacting with OpenFGA (Fine-Grained Authorization) API. This collection is based on the official OpenFGA API specifications:
- OpenAPI Spec: [OpenFGA API Swagger](https://raw.githubusercontent.com/openfga/api/main/docs/openapiv2/apidocs.swagger.json)
- API Documentation: [OpenFGA API Reference](https://openfga.dev/api/service)

## Getting Started

### Prerequisites
- [Postman](https://www.postman.com/downloads/) installed on your machine
- Valid OpenFGA authentication credentials

### Installation

1. Download both files from this repository:
   - `openfga-collection.json` (API collection)
   - `openfga-environment.json` (Environment variables)

2. Import into Postman:
   - Open Postman
   - Click "Import" (top left)
   - Upload both JSON files

I'll create a template for the environment variables and update the explanation in the README.

```json
{
  "name": "OpenFGA Environment",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://api.openfga.example.com",
      "type": "default",
      "enabled": true
    },
    {
      "key": "bearerToken",
      "value": "your-bearer-token-here",
      "type": "secret",
      "enabled": true
    },
    {
      "key": "storeId",
      "value": "your-store-id",
      "type": "default",
      "enabled": true
    },
    {
      "key": "authorizationModelId",
      "value": "your-authorization-model-id",
      "type": "default",
      "enabled": true
    },
    {
      "key": "pageSize",
      "value": "10",
      "type": "default",
      "enabled": true
    },
    {
      "key": "continuationToken",
      "value": "",
      "type": "default",
      "enabled": true
    }
  ]
}
```

And here's the updated section for the README:

### Environment Setup

1. Download the `openfga-environment.json` template
2. Modify the values according to your setup:
   ```json
   {
     "baseUrl": "Your OpenFGA API URL",
     "bearerToken": "Your JWT token",
     "storeId": "Your store ID",
     "authorizationModelId": "Your model ID",
     "pageSize": "Number of items per page (default: 10)",
     "continuationToken": "Leave empty initially"
   }
   ```
3. Import into Postman:
   - Click "Import" (top left)
   - Upload your modified JSON file
   - Or use the "Raw text" option and paste the JSON content
4. Select the imported environment from the environment dropdown (top right)

> **Note**: The `bearerToken` is marked as a "secret" type for additional security. Postman will treat this value with extra care and hide it in the UI.

## Authentication

This collection requires Bearer token authentication for all requests. Make sure to:
1. Obtain a valid bearer token from your authentication provider
2. Add it to the `bearerToken` environment variable
3. The collection will automatically include it in the request headers

## API Endpoints

The collection includes all endpoints from the official OpenFGA API:
- Stores API
- Authorization Models
- Relationship Tuples
- Check Operations
- Relationship Queries
- Related Object Operations

For detailed API documentation, refer to the [OpenFGA API Reference](https://openfga.dev/api/service).

## Usage Examples

Basic example of using an endpoint:
1. Select a request from the collection
2. Ensure your environment variables are set
3. Your bearer token will be automatically included
4. Send the request
