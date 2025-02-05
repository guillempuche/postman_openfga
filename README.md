# OpenFGA API Collection

Postman collection for OpenFGA API with environment setup. Ready-to-use requests for authorization model and relationship management. Includes example authorization models for:
- Document management (Google Drive-like)
- GitHub-style repository access
- Employee management system
- RBAC (Role-Based Access Control)
- Conference room booking system

This collection is based on the official OpenFGA API specifications:
- OpenAPI Spec: [OpenFGA API Swagger](https://raw.githubusercontent.com/openfga/api/main/docs/openapiv2/apidocs.swagger.json)
- API Documentation: [OpenFGA API Reference](https://openfga.dev/api/service)

## Getting Started

### Prerequisites
- [Postman](https://www.postman.com/downloads/) installed on your machine
- Valid OpenFGA authentication credentials

### Installation

1. Download these files from the repository:
   - `openfga-collection.json` (API collection)
   - `openfga-environment.json` (Environment variables template)

2. Set up environment:
   - Copy `openfga-environment.json` and rename it to `openfga-environment.json`
   - Modify the values according to your setup:
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
   - Open Postman
   - Click "Import" (top left)
   - Upload both JSON files
   - Select the imported environment from the environment dropdown (top right)

> **Note**: The `bearerToken` is marked as a "secret" type for additional security. Postman will treat this value with extra care and hide it in the UI.

## Example: Setting up a Document Management System

This example shows how to create a store, set up an authorization model for document management, and grant access to a user.

1. First, create a new store:
```http
POST {{baseUrl}}/stores
Content-Type: application/json

{
  "name": "document-management-store"
}

// Response will contain your store ID
{
  "id": "01FCNDV6P870EA6S7TK1DSYDG0",
  "name": "document-management-store",
  "created_at": "2024-02-05T12:00:00.000Z"
}
```

2. Create an authorization model for document management:
```http
POST {{baseUrl}}/stores/{{storeId}}/authorization-models
Content-Type: application/json

{
  "schema_version": "1.1",
  "type_definitions": [
    {
      "type": "user"
    },
    {
      "type": "document",
      "relations": {
        "reader": {
          "union": {
            "child": [
              {
                "this": {}
              },
              {
                "computedUserset": {
                  "relation": "writer"
                }
              }
            ]
          }
        },
        "writer": {
          "this": {}
        }
      }
    }
  ]
}

// Response will contain your authorization model ID
{
  "authorization_model_id": "01FCNDV6P870EA6S7TK1DSYDG0"
}
```

3. Write a relationship tuple to grant access:
```http
POST {{baseUrl}}/stores/{{storeId}}/write
Content-Type: application/json

{
  "writes": {
    "tuple_keys": [
      {
        "user": "user:anne",
        "relation": "writer",
        "object": "document:budget-2024"
      }
    ]
  }
}
```

4. Verify access:
```http
POST {{baseUrl}}/stores/{{storeId}}/check
Content-Type: application/json

{
  "tuple_key": {
    "user": "user:anne",
    "relation": "reader",
    "object": "document:budget-2024"
  },
  "authorization_model_id": "01FCNDV6P870EA6S7TK1DSYDG0"
}

// Response should show allowed: true because writers are also readers
{
  "allowed": true
}
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
