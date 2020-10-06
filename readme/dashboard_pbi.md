# Criar nossa dashboard no PBI para visualizar nossos dados em stream
___

Caso você ainda não tenha um tenant do M365 com o PBI, você pode criar um tenant trial com 25 licenças por 30 dias seguindo as etapas deste link: https://www.microsoft.com/pt-br/microsoft-365/enterprise/office-365-e5?activetab=pivot%3aoverviewtab. Basta clicar em **"Avaliação gratuita"** e preencher as solicitações conforme solicitadas.  

> 1. Primeiro abra esse link: https://powerbi.microsoft.com/en-us/ e click em **"Sign in"** em seguida entre com seu usuário e senha do tenant do seu PBI
- Uma vez logado você deve clicar em **"My workspace"**, depois em **"Datasets + dataflows"** encontre o seu Dataset e click nos 3 pontos verticais em seguida click em **"Edit"**. OBS: Se seu dataset não aparecer aqui, você deve gerar mais dados usando a etapa anterior para ele gerar seu dataset.

![img19](/img/pbi2.png)

> 2. Em **"Edit streaming dataset"** tenha certeza que o tipo de dados está de acordo com suas configurações feitas na query do **"Stream Analytics"**

![img20](/img/pbi3.png)

> 3. Agora novamente em **"My workspace"** click em **"+ New"** e em seguida selecione **"Dashboard"**

![img21](/img/pbi4.png)

> 4. Digite um nome para sua Dashboard ex: Data Workshop

> 5. Agora click em **"Edit"** em seguida click em **"+ Add a tile"** selecione **"REAL-TIME DATA"** e click em **"Next"** 

![img22](/img/pbi5.png)

> 6. Nesta etapa você deve selecionar o Dataset criado pelo **"Stream Analytics"** 

![img23](/img/pbi6.png)

> 7. Agora você pode selecionar as visualizações que precisar para sua Dashboard 

![img24](/img/pbi7.png)

## Próximo passo
___

[Criar nosso Azure Data Factory e transformar alguns dados](./data_factory.md)
