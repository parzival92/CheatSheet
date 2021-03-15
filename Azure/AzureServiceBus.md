## Azure Service Bus

Message type solution

Azure Service Bus can exchange messages in three different ways: queues, topics, and relays

### Create a Service Bus namespace

```
az servicebus namespace create --name ****** --subscription **** --resource-group ********** --location "East US" --sku Standard
```

### Create a Service Bus queue(Messages that relate to individual sales must be sent only to the web service instance in the user's region)

```
az servicebus queue create --name ****** --namespace-name ***** --resource-group ******
```

### Create a Service Bus topic and subscriptions(Messages that relate to sales performance must be sent to all instances of the web service.)

```
az servicebus topic create --name *** --namespace-name ****** --resource-group **** --enable-partitioning true

az servicebus topic subscription create --name Americas --namespace-name *** --resource-group ****** --max-delivery-count 100 --topic-name ****

```

Display the primary connection string for your Service Bus namespace

```
az servicebus namespace authorization-rule keys list \
    --resource-group ****** \
    --name RootManageSharedAccessKey \
    --query primaryConnectionString \
    --output tsv \
    --namespace-name <namespace-name>
```

Display Message count

```
az servicebus queue show \
    --resource-group ***** \
    --name ***** \
    --query messageCount \
    --namespace-name <namespace-name>
```