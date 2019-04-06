# ARM-External-Templates

## Scenarios

- [LinkedDeployments-Contributor](LinkedDeployments-Contributor)
- [LinkedDeployments-Owner](LinkedDeployments-Owner)

### Expectations

- [LinkedDeployments-Contributor](LinkedDeployments-Contributor) assumes that the deployment account only has **contributor** rights to a specific resource group (or subscription).  This is the more common deployment scenario.

- [LinkedDeployments-Owner](LinkedDeployments-Owner) assumes that the deployment account has **owner** rights to a subscription.  This is a less common deployment scenario (possibly development environment) as that account will be highly privilaged and have access to all resource groups.

- AzureRM.* PowerShell modules have been installed (or AZ.* modules with the Enable-AzureRMAlias command run).

### Deployment steps

1. Update each of the `*.parameters.json` files with the appropriate values.
1. Upload the `*.json` and `Update-AutomationAzureModulesForAccount.ps1` files to a blob storage account with public blob read access (for demo purposes only) granted.

    > **Note:** A more secure approach would be to update the **templateStorageContainerUriRoot** and **parametersStorageContainerUriRoot** parameters in `helloworldParent.parameters.json` file to use a SAS token to the storage account instead of assigning public blob read access.  This would require updating the SAS token frequently or using a long lived token.

1. Update `DeployTemplate-Contributor.ps1` or `DeployTemplate-Owner.ps1` with the appropriate region, resource group name (only for Contributor scenario), and deployment name.
1. Login to Azure PowerShell to the subscription desired.
1. Run `DeployTemplate-Contributor.ps1` or `DeployTemplate-Owner.ps1` from the context of the folder desired.