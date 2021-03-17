## Azure Storage

Application data can be classified in one of three ways: structured, semi-structured, and unstructured

* **Structured - Relational Database (SQL)**
* **semi-structured - NoSQl(Key/value/document/Grpah Databases)**
* **Unstructured - Media files, such as photos, videos, and audio files, log files**

Azure Storage Services
-----------------------
* **Azure Blobs**
* **Azure Files**
* **Azure Queues**
* **Azure Tables**

A single Azure subscription can host up to 200 storage accounts, each of which can hold 500 TB of data.

```
az storage account create \
  --resource-group <rgname> \
  --location eastus \
  --sku Standard_LRS \
  --name <name>
```

Query Storage Connection String

```
az storage account show-connection-string \
  --resource-group <rgname> \
  --query connectionString \
  --name <name>

```
## Azure Storage Queue

* **Create Storage Account**

```
az storage account create --name [unique-name] -g [resource-group-name] --kind StorageV2 --sku Standard_LRS

```

* **Get Connection String**

```
az storage account show-connection-string --name <name> --resource-group [resource-group-name]
```
## Azure Storage Security

* **Azure AD App permission**
* **Storage keys which will provide full access to storage accounts**
* **Shared Access Signatures ( Particular time frame access and limited access ,Good for third party services )**

## Control network access to your storage account

* **Manage default network access rules**


Go to Storage Account >> Networking >> To restrict traffic from selected networks, select Selected networks. To allow traffic from all networks, select All networks.
