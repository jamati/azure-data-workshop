# Criar seu Event Hub 

> 1. Criar o Event Hubs namespace

No portal do Azure Portal click em **"Create a resource"** e então digite **Event Hubs**. Click em **"Create"** e siga as configurações abaixo: 

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado na etapa anterior
- Namespace name: Digite um nome para seu namespace. ex: eventhubworkshop
- Location: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Pricing tier: Aqui você deve selecionar tier do Event Hub. Para esse workshop vou utilizar o "Standard".
- Throughput Units: Aqui você define quantas unidades são necessárias para nossa carga de trabalho. Para esse workshop vou utilizar "1"
- Click em **"Review + create"**

![img4](/img/eventhubs.png)
___

> 2. Agora você precisa criar o Event Hub 

Uma vez dentro do Event Hubs namespace que você acabou de criar click em **"+ Event Hub"** e então siga as configurações abaixo. Ao finalizar click em **"Create"**

- Name: Digite um nome para seu Event Hub. ex: eventhub1
- Partition Count: Vamos deixar o padrão **"1"**
- Message Retention: Vamos deixar o padrão **"1"**
- Capture: Selecione **"Off"**

![img5](/img/eventhub1.png)
![img6](/img/eventhub2.png)
___

## Próximo passo
___

[Criar nosso seu Data Lake, gerenciado e criar nossos containers](./data_lake.md)