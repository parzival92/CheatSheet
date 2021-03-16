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
