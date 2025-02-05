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

[Rest of the sections remain the same...]

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
