# Create an SPN via username and password for Azure DevOps

az cloud set --name AzureUSGovernment or AzureCloud
```SPN=$(az ad sp create-for-rbac -n "SPNName" --skip-assignment -o json)```
SPNScope="/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RG_Name>"

az role assignment create --role Contributor \
                          --assignee $(echo $SPN | jq -r '.appId') \
                          --scope $SPNScope

az ad sp create-for-rbac -n "SPNName" 
                         --role Contributor 
                         --scopes /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RG_Name> /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RG_Name>

# Verify SPN
az login --service-principal --username $(echo $SPN | jq -r '.appId') \
                             --password $(echo $SPN | jq -r '.password') \
                             --tenant   $(echo $SPN | jq -r '.tenant') 