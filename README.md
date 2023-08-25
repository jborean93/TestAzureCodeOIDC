# Test Azure OIDC Authentication

This is a test repo to test out Azure OIDC authentication with GitHub.
It is designed to give a skeleton workflow for building + signing a PowerShell module with a key in Azure Key Vault plus a publishing step.
See https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure and https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-portal%2Clinux for more information on OIDC auth with GitHub Actions and Azure.

The following GitHub secrets must be defined:

+ `AZURE_SUBSCRIPTION_ID` - The Azure subscription id guid the app is registered in
+ `AZURE_TENANT_ID` - The tenant id guid of the app registration
+ `AZURE_CLIENT_ID` - The client id guid of the app registration
+ `AZURE_VAULT_NAME` - The name of the Azure Key Vault the certificate is stored in
+ `AZURE_VAULT_CERT_NAME` - The name of the Azure Key Vault certificate

The federated credential is registered for this repo on the `main` branch as that is where the OIDC claim will be running as.
While you can use a branch, tag, or environment name, Azure does not support pattern matching so I cannot use the claim for tags that match `v*`.
In the end I decided on always signing the module when a commit to `main` is made and having a separate publish workflow that uses this artifact for publishing solving this problem.
In the future I might revisit this to see if I can lock it down even further and only have the claim be valid when it is a release tag.

The authenticode signing work is done by the [OpenAuthenticode](https://github.com/jborean93/PowerShell-OpenAuthenticode/tree/main) module.
See [Authenticode Azure Keys](https://github.com/jborean93/PowerShell-OpenAuthenticode/blob/main/docs/en-US/about_AuthenticodeAzureKeys.md) for more information on how the module can use a key stores in an Azure Key Vault.
It works seamlessly with the Azure OIDC login task to authenticate as a principal when retrieving a key without sharing any secrets.

Only secret left in the whole publishing process is the PowerShell Gallery nuget token.
Until the PSGallery supports OIDC then this is unavoidable.
