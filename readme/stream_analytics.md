# Criar seu Event Hub 

> 1. Vamos criar nosso Stream Analytics job

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

> 2. Agora vamos criar nossos Inputs Stream Analytics job

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

> 3. Agora vamos criar nossos Outputs Stream Analytics job

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

> 4. Agora vamos criar nossa **"Query"** do Stream Analytics job

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

**Obs.: Neste passo caso você queira testar as queries, será necessário gerar dados. Você pode ir ao próximo passo gerar os dados e retornar para testar as queries.**
___

> 5. Dentro do seu Stream Analytics job click em **"Start"** 

![img18](/img/streamstart1.png)

## Próximo passo

[Gerar dados simulados para serem consumidos pelo Event Hub](./event_hub.md)