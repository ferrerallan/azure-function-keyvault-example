
# Azure Function Key Vault Example

## Description

This repository provides an example of using Azure Functions with Azure Key Vault to securely manage secrets. It demonstrates how to set up and use Azure Key Vault to store and access secrets from an Azure Function, which is useful for developers looking to implement secure secret management in their serverless applications.

## Requirements

- Node.js
- Azure Account with Key Vault and Azure Functions setup
- Azure Functions Core Tools
- Azure CLI
- Yarn or npm for package management

## Mode of Use

1. Clone the repository:
   ```bash
   git clone https://github.com/ferrerallan/azure-function-keyvault-example.git
   ```
2. Navigate to the project directory:
   ```bash
   cd azure-function-keyvault-example
   ```
3. Install the dependencies:
   ```bash
   yarn install
   ```
4. Ensure you have an Azure account with Key Vault and Azure Functions setup.
5. Install Azure Functions Core Tools and Azure CLI.
6. Deploy the Azure Function:
   ```bash
   func azure functionapp publish <FunctionAppName>
   ```

## Implementation Details

- **functions/**: Contains the Azure Functions code for accessing Key Vault secrets.
- **package.json**: Configuration file for the Node.js project, including dependencies.
- **local.settings.json**: Configuration file for local development settings.

### Example of Use

Here is an example of how to access a secret from Azure Key Vault using an Azure Function:

```javascript
const {{ DefaultAzureCredential }} = require("@azure/identity");
const {{ SecretClient }} = require("@azure/keyvault-secrets");

const credential = new DefaultAzureCredential();
const vaultName = process.env.KEY_VAULT_NAME;
const url = `https://${{vaultName}}.vault.azure.net`;
const client = new SecretClient(url, credential);

module.exports = async function (context, req) {{
  const secretName = req.query.name || req.body.name;
  try {{
    const secret = await client.getSecret(secretName);
    context.res = {{
      status: 200,
      body: `The value of the secret is: ${{secret.value}}`
    }};
  }} catch (err) {{
    context.res = {{
      status: 500,
      body: `Error retrieving secret: ${{err.message}}`
    }};
  }}
}};
```

This code initializes a client to access Azure Key Vault, retrieves a secret based on the request parameters, and returns the secret's value.

## License

This project is licensed under the MIT License.

You can access the repository [here](https://github.com/ferrerallan/azure-function-keyvault-example).
