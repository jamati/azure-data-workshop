# Criar nosso Azure Data Factory e transformar dados

> 1. Criando o Azure Data Factory (ADF)

Dentro do seu resource group criado anteriormente click em **"+Add"** digite **Data Factory** então click em **"Create"** e siga as configurações abaixo:

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado nas etapas anteriores
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Name: Digite um nome para seu **"Data Factory"**. ex: dataworkshop 
- Version: Selecione **"V2"**

Click em **"Next: Git configuration"**

- Nesta etapa você pode configurar um repositório para seu código. Para esse workshop vamos marcar a opção **"Configure Git Later"** clicar em **"Review + create"** e em seguida clicar em **"Create"**

![img30](/img/datafactory1.png)

![img31](/img/datafactory2.png)
___

- Após a criação entre no seu **Data Factory** e click em **"Author & Monitor"**. Após clicar uma nova aba irá se abrir derecionando-o para o **Data Factory workspace**

![img32](/img/datafactory3.png)
___

> 2. Pipeline

- Agora é hora de criar nosso primeiro pipeline. Click em **"Create pipeline"**
- Name: Digite um nome para seu pipeline. ex: jason_to_CSV
- Click em **"Move & transform"** para expandir as opções. Agora arraste a opção **"Copy data"** para o espaço em branco do workspace.

![img33](/img/datafactory4.png)
___

- Agora vamos ligar nosso **"Data flow debug"** que é o cluster que irá executar nossas etapas de transformação dos nossos dados

![img34](/img/dataflowdebug1.png)
___

> 3. Source

- Agora click em **"Source"** e em seguida click em **"+ New"**
- Click em **"Azure"** em seguida selecione **"Azure Data Lake Storage Gen2"** e click em **"Continue"**

![img35](/img/datasource1.png)
___

- Selecione o formato do dado. Para esse workshop nosso source está em JSON então selecione **JSON** e click em **"Continue"**
- Agora em **"Set properties"** no campo **"Name"** digite um nome. ex: JSON e depois em **"Linked service"** selecione **"+ New"** e preencha as informações solicitadas
- Name: Digite um nome para seu linked service. ex: AzureDataLake_raw
- Azure Subscription: Selecione sua **subscrição**
- Storage account name: Selecione seu **Data Lake**
- Click em **"Test connection"** se a conexão for feita com sucesso click em **"Create"**

![img36](/img/datasource2.png)
___

- Em **"Set properties"** click no ícone da pasta e selecione seu container **rawdata** e depois click em **"OK"**

![img36](/img/datasource3.png)
___

- Em **"File path type"** selecione a opção **"Wildcard file path"**

![img37](/img/datasource4.png)
___

> 4. Sink 

- Agora click em **"Sink"** e em seguida click em **"+ New"**
- Click em **"Azure"** em seguida selecione **"Azure Data Lake Storage Gen2"** e click em **"Continue"**
- Selecione o formato do dado. Para esse workshop nosso sink será em csv então selecione **CSV** e click em **"Continue"**
- Agora em **"Set properties"** no campo **"Name"** digite um nome. ex: CSV e depois em **"Linked service"** selecione **"+ New"** e preencha as informações solicitadas
- Name: Digite um nome para seu linked service. ex: AzureDataLake_transformeddata
- Azure Subscription: Selecione sua **subscrição**
- Storage account name: Selecione seu **Data Lake**
- Click em **"Test connection"** se a conexão for feita com sucesso click em **"Create"**
- Em **"Set properties"** click no ícone da pasta e selecione seu container **transformeddata** e depois click em **"OK"**
- Em **""File extension"** altere para **".csv"**

![img38](/img/sinkdata1.png)
___

- E dentro do seu dataset **"csv"** em **"Connection"** marque a opção **"First row as header"**

![img39](/img/sinkdata2.png)
___

- Click em **"Schema"** e em seguida click em **"Import schema"**. Você já deve conseguir visualizar as colunas do seu arquivo CSV

![img40](/img/sinkdata3.png)
___

- Agora click em **"Mapping"** e verifique se o schema de dados está OK.

![img41](/img/datamapping1.png)
___

> 5. Agora vamos executar nosso pipeline

- Agora é só clicar em **"Debug"**. Para o debug funcionar o **"Data flow debug"** tem que estar ligado.

![img42](/img/debug1.png)

![img43](/img/debug2.png)
___

> 6. Agora você já pode verificar seus dados transformados utilizando o **Azure Storage Explorer**

![img44](/img/explorer4.png)
___

## Próximo passo

[Criar nosso Azure Machine Learning e criar nosso modelo de predição](./ml.md)