# Azure Storage Blob Upload from a Node.js Web Application

This sample demonstrates how to use the Azure Storage SDK in the context of an [Express](https://expressjs.com/) application to upload images into Azure Blob Storage.

## Getting started

Clone the repository to your machine:

```bash
git clone https://github.com/Azure-Samples/storage-blob-upload-from-webapp-node.git
```

Change into the `storage-blob-upload-from-webapp-node` folder:

```bash
cd storage-blob-upload-from-webapp-node
```

Install dependencies via `npm`:

```bash
npm install
```

## Adding a connection string

Navigate to the [Azure Portal](https://portal.azure.com) and copy the connection string from your storage account (under **Settings** > **Access keys**) in to the `.env.example` file. Once you have pasted your connection string in to the file, rename the file from `.env.example` to `.env`.

## Running the sample

Start the server:

```bash
npm start
```

Navigate to [http://localhost:3000](http://localhost:3000) and upload an image to blob storage.

You can use the [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) to view blob containers and verify your upload is successful.



az group create -n nodesample -l japaneast

az storage account create -n nodesample1023a \
-l japaneast -g nodesample \
--sku Standard_LRS --kind blobstorage --access-tier hot

# Containerの作成
blobStorageAccount=nodesample1023a

blobStorageAccountKey=$(az storage account keys list -g nodesample -n nodesample1023a --query '[0].value' --output tsv)

az storage container create -n images --account-name $blobStorageAccount \
--account-key $blobStorageAccountKey --public-access container

az storage container create -n thumbnails --account-name $blobStorageAccount \
--account-key $blobStorageAccountKey --public-access container

echo "Make a note of your blob storage account key..."
echo $blobStorageAccountKey

