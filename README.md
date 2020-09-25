# Azure Data Workshop 
Este workshop contém instruções sobre como criar os recursos necessários para fazer a ingestão dos dados até a apresentação conforme a arquitetura abaixo:

![img1](/img/arquitetura.png)

## Praparar o ambiente ##

> 1. Crie sua conta gratuita no Azure

Basta seguir o passo a passo do link abaixo. Obs: Utilize um email para criar sua conta Microsoft que nunca tenha utilizado para trial do Azure anteriormente.
Link: https://azure.microsoft.com/pt-br/free/
___

> 2. Criar um Resource Group

No portal do Azure Portal click em **"Create a resource"** e então digite **Resource Group** . Click em **"Create"** 

- Subscription: Selecione sua subscrição
- Resource group: Digite um nome para o sue resource. Ex: data-workshop
- Selecione uma região. Aqui você pode utilizar qualquer região disponível.   

![img2](/img/resourcegroup.GIF)

![img3](/img/resourcegroup.png)

___

> 3. Criar o Event Hubs namespace

No portal do Azure Portal click em **"Create a resource"** e então digite **Event Hubs** . Click em **"Create"** e siga as configurações abaixo: 

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado na etapa anterior
- Namespace name: Digite um nome para seu namespace. ex: eventhubworkshop
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Pricing tier: Aqui você deve selecionar tier do Event Hub. Para esse workshop vou utilizar o "Standard".
- Throughput Units: Aqui você define quantas unidades são necessárias para nossa carga de trabalho. Para esse workshop vou utilizar "1"

![img4](/img/eventhubs.png)

### Agora você precisa criar o Event Hub ###

Uma vez dentro do Event Hubs namespace que você acabou de criar click em **"+ Event Hub"** e então siga as configurações abaixo e depois click em **"Create"**

- Name: Digite um nome para seu Event Hub. ex: eventhub1
- Partition Count: Selecione o resource group criado na etapa anterior
- Message Retention: Digite um nome para seu namespace. ex: eventhubworkshop
- Capture: Selecione **"Off"**

![img5](/img/eventhub1.png)
![img6](/img/eventhub2.png)

___

> 4. Criar o seu Data Lake

Dentro do seu resource group criado anteriormente click em **"+Add"** digite **Storage Account** então click em **"Create"** e siga as configurações abaixo:

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado anteriormente
- Storage account name: Digite um nome para sua storage account. ex: datalakeworkshop
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Performance: Aqui você deve selecionar performance. Para esse workshop vou utilizar o **"Standard"**.
- Account kind: Aqui você deve selecionar o tipo. Para esse workshop vou utilizar **"StorageV2"**
- Replication: Aqui você deve selecionar o tipo de replicação. Para esse workshop vou utilizar **"Locally-redundant storage"**
- Blob access tier: Aqui você seleciona o tipo de acesso. Para esse workshop vou utilizar **"Hot"**

- Após preencher os campos click em **"Next: Networking"**

![img7](/img/storageaccount.GIF)

![img8](/img/storageaccount1.png)

- Em **"Networking"** deixe as opções padrão e click em **"Next: Data protection"**

![img9](/img/storageaccount2.png)

- Em **"Data protection"** deixe as opções padrão e click em **"Next: Advanced"** 

![img10](/img/storageaccount3.png)

- Em **"Advanced"** na opção **"Data Lake Storage Gen2"** click em  **"Enabled"** e depois click em **"Review + Create"**, após o review click em **"Create"**

![img11](/img/storageaccount04.png)


___

> 5. Gerenciar meu Azure Data Lake com o Azure Storage Explorer 

- Click neste link https://azure.microsoft.com/en-us/features/storage-explorer/ e baixe o **"Azure Storage Explorer"**. 
- Após abrir o aplicativo log utilizando suas credenciais do Azure
- Uma vez logado encontre o Data Lake que você acabou de criar
- Click com o botão da direita do mouse e click em **"Create Blob Container"**

![img12](/img/explorer1.png)

- Crie dois **"Blob Containers"** um chamado **"rawdata"** e outro **"transformeddata"**

![img13](/img/explorer2.png)

