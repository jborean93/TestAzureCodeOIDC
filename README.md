# Test Azure OIDC Authentication

This is a test repo to test out Azure OIDC authentication with GitHub.
It is designed to give a skeleton workflow for building + signing a PowerShell module wit a key in Azure Key Vault plus a publishing step.
See https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure and https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-portal%2Clinux for more information on OIDC auth with GitHub Actions and Azure.

The following GitHub secrets must be defined:

+ `AZURE_SUBSCRIPTION_ID` - The Azure subscription id guid the app is registered in
+ `AZURE_TENANT_ID` - The tenant id guid of the app registration
+ `AZURE_CLIENT_ID` - The client id guid of the app registration
+ `AZURE_VAULT_NAME` - The name of the Azure Key Vault the certificate is stored in
+ `AZURE_VAULT_CERT_NAME` - The name of the Azure Key Vault certificate
