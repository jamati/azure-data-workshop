# Azure Data Workshop (Preview) :stuck_out_tongue_winking_eye:
Este workshop contém instruções sobre como criar os recursos necessários para fazer da ingestão dos dados até a apresentação conforme a arquitetura abaixo:

![img1](/img/arquitetura.png)

## Criando o ambiente ##

> 1. Crie sua conta gratuita no Azure

Basta seguir o passo a passo do link abaixo. Obs: Utilize um email para criar sua conta Microsoft que nunca tenha utilizado para trial do Azure anteriormente.
Link: https://azure.microsoft.com/pt-br/free/
___

> 2. Criar um Resource Group

No portal do Azure Portal click em **"Create a resource"** e então digite **Resource Group** . Click em **"Create"** 

- Subscription: Selecione sua subscrição
- Resource group: Digite um nome para o sua resource. ex: data-workshop
- Region: Aqui você pode utilizar qualquer região disponível.   

![img2](/img/resourcegroup.GIF)

![img3](/img/resourcegroup.png)

___

> 3. Criar o Event Hubs namespace

No portal do Azure Portal click em **"Create a resource"** e então digite **Event Hubs**. Click em **"Create"** e siga as configurações abaixo: 

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado na etapa anterior
- Namespace name: Digite um nome para seu namespace. ex: eventhubworkshop
- Location: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Pricing tier: Aqui você deve selecionar tier do Event Hub. Para esse workshop vou utilizar o "Standard".
- Throughput Units: Aqui você define quantas unidades são necessárias para nossa carga de trabalho. Para esse workshop vou utilizar "1"
- Click em **"Review + create"**

![img4](/img/eventhubs.png)

### Agora você precisa criar o Event Hub ###

Uma vez dentro do Event Hubs namespace que você acabou de criar click em **"+ Event Hub"** e então siga as configurações abaixo. Ao finalizar click em **"Create"**

- Name: Digite um nome para seu Event Hub. ex: eventhub1
- Partition Count: Vamos deixar o padrão **"1"**
- Message Retention: Vamos deixar o padrão **"1"**
- Capture: Selecione **"Off"**

![img5](/img/eventhub1.png)
![img6](/img/eventhub2.png)

___

> 4. Criar o seu Data Lake

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

> 5. Gerenciar meu Azure Data Lake com o Azure Storage Explorer 

- Click neste link https://azure.microsoft.com/en-us/features/storage-explorer/ e baixe o **"Azure Storage Explorer"**. 
- Após abrir o aplicativo log utilizando suas credenciais do Azure
- Uma vez logado encontre o Data Lake que você acabou de criar
- Click com o botão da direita do mouse e click em **"Create Blob Container"**

![img10](/img/explorer1.png)

- Crie dois **"Blob Containers"** um chamado **"rawdata"** e outro **"transformeddata"**

![img11](/img/explorer2.png)

___

> 6. Vamos criar nosso Stream Analytics job

Dentro do seu resource group criado anteriormente click em **"+Add"** digite **Stream Analytics job** então click em **"Create"** e siga as configurações abaixo:

- Job Name: Digite um nome para seu Job. ex: streamdataworkshop 
- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado anteriormente
- Location: Selecione uma região onde será feito o deployment do seu Job. Recomendo East US por questões de custos.
- Hosting environment: Selecione **"Cloud"**
- Streaming units: Deixe o padrão **"3"**
- Click em **"Create"**

![img12](/img/stream01.png)

___

> 7. Agora vamos criar nossos Inputs e Outputs do Stream Analytics job

### Inputs ###

Dentro do seu Stream Analytics job click em **"Inputs"** em seguida click em **"+ Add stream input"** e selecione **"Event Hub"**

- Input alias: Digite um nome para seu Job. ex: eventhubinput
- Use a opção **"Select Event Hub from your subscriptions"**
- Subscription: Selecione sua subscrição
- Event Hub namespace: Selecione o seu Event Hub namespace criado nas etapas anteriores
- Event Hub name: Selecione **"Use existing"** e selecione o Event Hub criado anteriormente
- Event Hub policy name: Selecione **"Create new"** e pode deixar o nome sugerido ou alterar para o nome que desejar
- Event Hub consumer group: Selecione **"Create new"** e pode deixar o nome sugerido ou alterar para o nome que desejar
- Partition Key: Pode deixar esse campo em branco para esse workshop
- Event serialization format: Deixar o padrão **"JSON"**
- Encoding: Deixar o padrão **"UTF-8"**
- Event compression type: Deixar o padrão **"Nome"**
- Click em **"Save"**

![img13](/img/input1.png)

![img14](/img/input2.png)

___

### Agora para Output ### 

Novamente dentro do seu Stream Analytics job click em **"Outputs"** em seguida click em **"+ Add"** e selecione **"Blob storage/ADLS Gen2"**

- Use a opção **"Select storage from your subscriptions"**
- Subscription: Selecione sua subscrição
- Storage account: Selecione a sua Storage account criada nas etapas anteriores
- Container: Selecione **"Use existing"** e selecione o container **"rawdata"** criado anteriormente
- Path pattern: Digite **{date}** 
- Data format: Selecione o padrão **YYYY/MM/DD**
- Event serialization format: Deixar o padrão **"JSON"**
- Encoding: Deixar o padrão **"UTF-8"**
- Format: Selecione **"Line separated"**
- Minimum rows: Digite **"1"**
- Maximum time: Para Hours digite **"0"** e para Minutes digite **"5"**
- Authentication mode: Selecione **"Connection string"**
- Click em **"Save"**

![img15](/img/input3.png)

___

Mais uma vez dentro do seu Stream Analytics job click em **"Outputs"** em seguida click em **"+ Add"** selecione **"Power BI"** e click em **"Authorize"**
Utilize as credenciais do seu tenant para logar no Power BI, depois siga as configurações abaixo:

- Output alias: Digite um nome para seu Job. ex: pbioutput
- Group workshop: Selecione **"My workspace"**. Obs: Caso não apareça essa opção, em "Authentication mode: Selecione **"User token"**
- Dataset name: Digite um nome para seu Dataset. ex: dataworkshop 
- Table name: Digite um nome para seu Dataset. ex: dataworkshop 
- Authentication mode: Selecione **"User token"** caso não tenha feito anteriormente.
- Click em **"Save"**

![img16](/img/output1.png)

___

### Query ###

Novamente dentro do seu Stream Analytics job click em **"Edit query"** utilize o código abaixo e click em **"Save"**. Obs: Dentro da query nos commands INTO e FROM tem que estar de acordo com o nome dos inputs e outputs que você criou.


```
SELECT
    TRY_CAST (sensor_temp as bigint) as Temperatura,
    TRY_CAST (sensor_id as bigint) as SensorID,
    TRY_CAST (sensor_hum as bigint) as Umidade,
    TRY_CAST (sensor_status as nvarchar(max)) as Status,
    TRY_CAST (EventEnqueuedUtcTime as datetime) as Data_Hora
INTO
    datalakeoutput
FROM
    eventhubinput

SELECT
    TRY_CAST (sensor_temp as bigint) as Temperatura,
    TRY_CAST (sensor_hum as bigint) as Umidade,
    TRY_CAST (EventEnqueuedUtcTime as datetime) as Data_Hora
    
INTO
    pbioutput
FROM
    eventhubinput
```

![img17](/img/query1.png)

- Click em **"Save query"**

___

Dentro do seu Stream Analytics job click em **"Start"** 

![img18](/img/streamstart1.png)

___

> 8. Agora vamos simular dados entrando no nosso Event Hub 

- Primeiro vamos simular alguns dados através deste link: https://eventhubdatagenerator.azurewebsites.net/
- No campo **"Event Hub Connection String"** preencha com os dados da sua connection string localizada aqui:
![img25](/img/connectionstring1.png)
- No campo **"Event Hub Namespace"** preencha com o nome do seu Event Hub namespace:
![img26](/img/namespace1.png)
- No campo **"Number of messanges"** digite **5**
- No campo **"Fake Data Methods"** preencha com o código abaixo:

```
            {
                "sensor_id":{
                  "faker": {
                    "fake": "{{random.number(100)}}"
                  }
                },
                "sensor_temp": {
                  "type": "integer", "minimum": "5", "maximum": "45"
                },
                "sensor_hum": {
                  "type": "integer", "minimum": "10", "maximum": "100"
                },
                "sensor_status": {
                  "type": "string",
                  "faker": {
                    "random.arrayElement": [["OK", "WARN", "FAIL"]]
                  }
                }
              }
```
![img27](/img/geradormensagem1.png)
- Click em **"Submit"**

Isto irá gerar 5 mensagens que serão consumidas pelo seu Event Hub. As mesmas já podem ser vistas na sua Dashboard do PBI e também dentro do seu Data Lake.

Você pode repetir esse processo quantas vezes quiser para gerar mais dados.

![img28](/img/pbi8.png)

![img29](/img/explorer3.png)

___

> 9. Agora criar seu Dashboard no PBI (Power BI) 

- Primeiro abra esse link: https://powerbi.microsoft.com/en-us/ e click em **"Sign in"** em seguida entre com seu usuário e senha do tenant do seu PBI
- Uma vez logado você deve clicar em **"My workspace"**, depois em **"Datasets + dataflows"** encontre o seu Dataset e click nos 3 pontos verticais em seguida click em **"Edit"**

![img19](/img/pbi2.png)
- Em **"Edit streaming dataset"** tenha certeza que o tipo de dados está de acordo com suas configurações feitas na query do **"Stream Analytics"**

![img20](/img/pbi3.png)
- Agora novamente em **"My workspace"** click em **"+ New"** e em seguida selecione **"Dashboard"**

![img21](/img/pbi4.png)
- Digite um nome para sua Dashboard ex: Data Workshop
- Agora click em **"Edit"** em seguida click em **"+ Add a tile"** selecione **"REAL-TIME DATA"** e click em **"Next"** 

![img22](/img/pbi5.png)
- Nesta etapa você deve selecionar o Dataset criado pelo **"Stream Analytics"** 

![img23](/img/pbi6.png)
- Agora você pode selecionar as visualizações que precisar para sua Dashboard 

![img24](/img/pbi7.png)

___

> 10. Vamos criar nosso Data Factory para fazer a orquestração dos dados

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

- Após a criação entre no seu **Data Factory** e click em **"Author & Monitor"**. Após clicar uma nova aba irá se abrir derecionando-o para o **Data Factory workspace**

![img32](/img/datafactory3.png)

### Pipeline ###
- Agora é hora de criar nosso primeiro pipeline. Click em **"Create pipeline"**
- Name: Digite um nome para seu pipeline. ex: jason_to_CSV
- Click em **"Move & transform"** para expandir as opções. Agora arraste a opção **"Copy data"** para o espaço em branco do workspace.

![img33](/img/datafactory4.png)

- Agora vamos ligar nosso **"Data flow debug"** que é o cluster que irá executar nossas etapas de transformação dos nossos dados

![img34](/img/dataflowdebug1.png)

### Source ###
- Agora click em **"Source"** e em seguida click em **"+ New"**
- Click em **"Azure"** em seguida selecione **"Azure Data Lake Storage Gen2"** e click em **"Continue"**

![img35](/img/datasource1.png)

- Selecione o formato do dado. Para esse workshop nosso source está em JSON então selecione **JSON** e click em **"Continue"**
- Agora em **"Set properties"** no campo **"Name"** digite um nome. ex: JSON e depois em **"Linked service"** selecione **"+ New"** e preencha as informações solicitadas
- Name: Digite um nome para seu linked service. ex: AzureDataLake_raw
- Azure Subscription: Selecione sua **subscrição**
- Storage account name: Selecione seu **Data Lake**
- Click em **"Test connection"** se a conexão for feita com sucesso click em **"Create"**

![img36](/img/datasource2.png)

- Em **"Set properties"** click no ícone da pasta e selecione seu container **rawdata** e depois click em **"OK"**

![img36](/img/datasource3.png)

- Em **"File path type"** selecione a opção **"Wildcard file path"**

![img37](/img/datasource4.png)

### Sink ###
- Agora click em **"Sink"** e em seguida click em **"+ New"** ### 
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

- E dentro do seu dataset **"csv"** em **"Connection"** marque a opção **"First row as header"**

![img39](/img/sinkdata2.png)

- Click em **"Schema"** e em seguida click em **"Import schema"**. Você já deve conseguir visualizar as colunas do seu arquivo CSV

![img40](/img/sinkdata3.png)

- Agora click em **"Mapping"** e verifique se o schema de dados está OK.

![img41](/img/datamapping1.png)

### Agora vamos executar nosso pipeline. ###

- Agora é só clicar em **"Debug"**

![img42](/img/debug1.png)

![img43](/img/debug2.png)

- Agora você já pode verificar seus dados transformados utilizando o **Azure Storage Explorer**

![img44](/img/explorer4.png)

___
