# Criar nosso seu Data Lake, gerenciado e criar nossos containers

> 1. Criar o seu Data Lake

Dentro do seu resource group criado anteriormente click em **"+Add"** digite **Storage Account** click em **"Create"** e então siga as configurações abaixo:

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado anteriormente
- Storage account name: Digite um nome para sua storage account. ex: datalakeworkshop
- Location: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Performance: Aqui você deve selecionar performance. Para esse workshop vou utilizar o **"Standard"**.
- Account kind: Aqui você deve selecionar o tipo. Para esse workshop vou utilizar **"StorageV2"**
- Replication: Aqui você deve selecionar o tipo de replicação. Para esse workshop vou utilizar **"Locally-redundant storage"**
- Blob access tier: Aqui você seleciona o tipo de acesso. Para esse workshop vou utilizar **"Hot"**

- Após preencher os campos click na aba superior **"Advanced"**

![img7](/img/storageaccount.GIF)

![img8](/img/storageaccount01.png)

- Em **"Advanced"** na opção **"Data Lake Storage Gen2"** click em  **"Enabled"** e depois click em **"Review + Create"**, após o review click em **"Create"**

![img9](/img/storageaccount04.png)
___

> 2. Agora vamos cópiar a **"Access Key"**

- Após a criação da sua Storage Account entre na mesma e click em **"Access Key"**

![img10](/img/storageaccount4.png)

- Cópie a **"Key 1"** em um notepad, pois vamos utilizá-la mais a frente

![img11](/img/storageaccount5.png)

> 3. Gerenciar meu Azure Data Lake com o Azure Storage Explorer 

- Click neste link https://azure.microsoft.com/en-us/features/storage-explorer/ e baixe o **"Azure Storage Explorer"**. 
- Após abrir o aplicativo log utilizando suas credenciais do Azure
- Uma vez logado encontre o Data Lake que você acabou de criar
- Click com o botão da direita do mouse e click em **"Create Blob Container"**

![img12](/img/explorer1.png)

- Crie dois **"Blob Containers"** um chamado **"rawdata"** e outro **"transformeddata"**

![img13](/img/explorer2.png)
___

## Próximo passo
___

[Criando seu Stream Analytics e configurar nossos inputs e outputs](./stream_analytics.md)