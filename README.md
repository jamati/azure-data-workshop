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
- Resource group: Digite um nome para o sue resource. Ex: MeuML
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
![img5](/img/eventhub1.png)

___

> 4. Criar o Event Hub

Uma vez dentro do Event Hubs namespace que você acabou de criar click em **"+ Event Hub"** e então siga as configurações abaixo: 

- Name: Digite um nome para seu Event Hub. ex: eventhub1
- Partition Count: Selecione o resource group criado na etapa anterior
- Message Retention: Digite um nome para seu namespace. ex: eventhubworkshop
- Capture: Selecione **"Off"**

![img6](/img/eventhub2.png)