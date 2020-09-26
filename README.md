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

![img12](/img/stream01.png)

___

> 7. Agora vamos criar nossos Inputs e Outputs do Stream Analytics job

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

Novamente dentro do seu Stream Analytics job click em **"Inputs"** em seguida click em **"+ Add stream input"** e selecione **"Blob storage/ADLS Gen2"**

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
- Group workshop: Selecione **"My workshop"**
- Dataset name: Digite um nome para seu Dataset. ex: dataworkshop 
- Table name: Digite um nome para seu Dataset. ex: dataworkshop 
- Authentication mode: Selecione **"User token"** 
- Click em **"Save"**

![img16](/img/output1.png)

___

Novamente dentro do seu Stream Analytics job click em **"Edit query"** utilize o código abaixo e click em **"Save"**


```
SELECT
    TRY_CAST (sensor_temp as bigint) as Temperatura,
    TRY_CAST (sensor_id as bigint) as SensorID,
    TRY_CAST (sensor_hum as bigint) as Humidade,
    TRY_CAST (sensor_status as nvarchar(max)) as Status,
    TRY_CAST (EventProcessedUtcTime as datetime) as Data_Hora
INTO
    datalakeoutput
FROM
    eventhubinput

SELECT
    TRY_CAST (sensor_temp as bigint) as Temperatura,
    TRY_CAST (sensor_id as bigint) as SensorID
    
INTO
    pbioutput
FROM
    eventhubinput
```

![img17](/img/query1.png)

___

Dentro do seu Stream Analytics job click em **"Start"** utilize o código abaixo e click em **"Save"**

![img18](/img/streamstart1.png)

___

> 8. Agora vamos simular dados entrando no nosso Event Hub e visualizá-los no PBI e no nosso Datalake

- Primeiro vamos simular alguns dados através deste link: https://eventhubdatagenerator.azurewebsites.net/
- No campo **"Event Hub Connection String"** preencha com os dados da sua connection string localizada aqui:
![img19](/img/connectionstring1.png)
- No campo **"Event Hub Namespace"** preencha com o nome do seu Event Hub namespace:
![img20](/img/namespace1.png)
- No campo **"Number of messanges"** digite **1000**
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
![img21](/img/geradormensagem1.png)
- Click em **"Submit"**

Isto irá gerar 1000 mensagens que serão consumidas pelo seu Event Hub