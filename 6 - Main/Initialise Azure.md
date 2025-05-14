2025-03-12 11:11

Status:

Tags:

---

# Install Azure CLI
az login
az group create --name factorysim-rg --location eastus

# Create PostgreSQL database
az postgres flexible-server create --name factorysimdb --resource-group factorysim-rg --admin-user dbuser --admin-password Week7890

# Create Event Hubs (Kafka alternative)
az eventhubs namespace create --name factorysim-events --resource-group factorysim-rg --sku Basic
az eventhubs eventhub create --name sensor --resource-group factorysim-rg --namespace-name factorysim-events

# Create Storage Account for CSV files
az storage account create --name factorysimfiles --resource-group factorysim-rg --kind StorageV2


##### References
----
