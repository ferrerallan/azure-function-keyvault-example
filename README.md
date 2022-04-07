# azure-function-keyvault-example
Simple example of Azure Function accessing a keyvault

# Requirements
-You need to have a free account of Azure
-Create a key secret for the desired value. For instance.. database connections, api
-Add Packages to use vault:
dotnet add package Azure.Identity
dotnet add package Azure.Security.KeyVaults.Secrets
dotnet add package Azure.Extensions.AspNetCore.Configuration.Secrets
-Add a new node into config as follow:
},
  "KeyVaultConfig":{
    "KVUrl":"URL",
    "TenantId":"Tenat",
    "ClientId":"client",
    "ClientSecretId":"clientSecretApp"
  },
-Register an application in App registration to get TenantID and clientID
-Give permission to application access this configuration.
Go to Keyvault=>Access policies
-Choose Secret Management
