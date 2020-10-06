# Criar nosso Azure Machine Learning e criar nosso modelo de predição

> 1. Nesta última etapa vamos consumir os dados já modificados na etapa anterior para criar nosso modelo preditivo utilizando Azure Machine Learning

Dentro do seu resource group criado anteriormente click em **"+Add"** digite **Machine Learning** então click em **"Create"** e siga as configurações abaixo:

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado nas etapas anteriores
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US por questões de custos.
- Click em **"Review + create"**

![img45](/img/ml01.png)

- Agora click no ícone do seu **Machine Learning**

![img46](/img/ml02.png)

- Agora click em **"Launch studio**

![img47](/img/ml03.png)

> 2. Agora você já está dentro do Azure Machine Learning Studio 

Click em **"Automated ML (preview)"** e então click no sinal de + conforme imagens abaixo:

![img13](/img/automated01.PNG)
___

> 3. Criar seu dataset

- Click em **"Create dataset"** e em seguida selecione **"From datastore"**

- Agora no janela que se abriu siga os as configurações abaixo:

    - Digite um nome para o seu dataset
    - Digite uma descrição para o seu dataset
    - Em seguida click em **"Next"**

    ![img16](/img/mldataset1.png)

    - Em **'Datastore selection'** selecione **"Create new datastore"** e siga as configurações abaixo:

        - Digite um nome para seu datastore
        - Deixe selecionado **"Azure Blob Storage"**
        - Deixe selecionado **"From Azure subscription"**
        - Deixe selecionado sua subscription
        - Selecionar o Storage Account que foi criado anteriormente
        - Selecionar o "Container" **"transfromeddata"** que você criou na 3º etapa desde workshop
        - Deixe selecionado **"Account Key"**
        - Em Account Key você deve colar a Key copiada na etapa 3 do workshop
        - Click em **'Create datastore'**

        ![img17](/img/mldataset2.png)

        - Agora click em **'Browser'** e clique nas pastas até encontrar o arquivo CSV criado na etapa 7 do Data Factory

       - Click em **'Next'**

        ![img18](/img/mldataset3.png)
        ___

        >3. 1 - Configurar seus dados

        - No campo **'Column headers'** selecione **'Use headers from the first file'** e em seguida click em **"Next"**

        ![img19](/img/mldataset4.png)
        ___

        > 3. 2 - Vamos configurar o esquema dos dados
        
        - Você precisa configurar colunas com o tipo correto de dados. **'String'** para colunas que contêm palavras e **'Integer'** para as colunas que contêm números conforme imagem abaixo:

        ![img19](/img/mldataset5.png)
        
        - Em seguida click em **'Next'**
        ___

        > 3. 3 - Confirmar os detalhes

        - Aqui basta confirmar as informações e click em **'Create'** 
        ___

> 4. Selecionar o dataset

- Agora que você já criou seu dataset selecione ele e click em **'Next'**

![img20](/img/mldataset6.png)
___

> 5. Configurar seu experimento

- Para rodar seu experimento, primeiro você precisa configurar um cluster para processar seus modelos

    - Digite um nome para seu experimento. Ex.: data_workshop
    - Em **'Target column'** você deve selecionar a coluna que deseja prever os valores. No nosso caso selecione **'Status'**
    - Click em **'Create a new compute'**

        - Digite um nome para seu cluster. Ex.: dataworkshop
        - No campo **'Virtual Machine type'** deixe selecionado **'CPU'**
        - No campo **'Virtual Machine priority'** deixe selecionado **'Dedicated'**
        - No campo **'Virtual Machine size'** deixe selecionado **'Standard_DS3_v2'**
        - No campo **'Minimum number of nodes'** deixe **'0'**
        - No campo **'Maximum number of nodes'** deixe **'3'**
        - No campo **'Idle seconds before scale down'** deixe em **'120'**
        - Click em **'Create'**

        ![img21](/img/newcluster01.png)

- Em **'Select computer cluster'** selecione o cluster que criou na etapa anterior
- Click em **'Next'**

![img22](/img/mlexperiment1.png)
___

> 6. Selecione qual tipo de problema quer resolver

- Aqui você deve entender qual tipo de problema precisa resolver. Algoritmos de Classificação são usado para responder "Sim ou Não", "Grupo A ou Grupo B", etc. Já os algoritmos de Regressão deve ser utilizado quando você busca um valor númerico "valor de um carro" baseado em algumas caracteristicas. Já nos algoritmos de Time series forecasting você utiliza para tentar prever o resultado de vendas baseado nos dados de vendas do passado. No nosso experimento vamos utilizar **'Classification'** 

- Click em **'Finish'**

![img23](/img/mltasktype1.png)
___

> 7. Vamos verificar os resultados

- Seu experimento está completo entao vamos verificar os resultado

- Como pode ser visto em **'Details'** o algoritmo escolhido foi o **'VotingEnsemble'** e obteve uma acurácia de 36.6%. **OBS.: Essa acurácia vai ficar baixa mesmo, pois estamos utilizando dados randômicos e isto nos impede de ter um melhor resultado. Nosso objetivo aqui é apenas seguir os passos para criar nosso modelo.***

![img24](/img/experiment2.png)

 - Click em **'Data guardralls'**
 
    - Aqui você verifica todas as etapas que foram executadas nos dados. Das alterações no esquema de dados a separação dos dados para treinamento e validação tudo pode ser visto aqui.
    
 - Click em **'Models'**

    - Aqui você consegue visualizar todos os algoritmos testados com a acurácia, tempo de execução, etc. Você pode verificar também que você rodou o modelo utilizando o **'Run 1'**, mas ele tem vários filhos e cada filho roda de forma independente e tem seu próprio número.
    - Você pode verificar em qualquer algoritmo para ver mais detalhes, e para ver seus detalhes basta click em **'Explain model'**
    - No algoritmo com melhor acurária no nosso caso o **'VotingEnsemble'** ja está habilitado o **'View explanation'** click nele. Ele irá te redirecionar para o **'Run 49'**

     ![img25](/img/mlresults1.png)

    - No **'Explanations'** você consegue verificar quais colunas (features) tiveram o maior impacto no seu modelo.

    ![img26](/img/mlexplanation1.png)

    - Click me **'Metrics'** para poder visualizar algumas métricas do seu modelo

    ![img27](/img/mlmetrics1.png)

    - Em **Output + logs'** é possível verificar todos os logs de execução e seus outputs.

    - Em **'Imagens'** caso seu modelo trabalhe com imagens mostraria aqui

    - Em **'Snapshot'** você consegue visualizar a execução do modelo em código python

- Click em **'Model'** 

![img28](/img/mlmodels1.png)
___

> 8. Agora é hora de fazer deploy do nosso modelo

Quando estiver satisfeito com os resultados do seu modelo é hora de fazer o deploy 

- Click em **'Deploy'**

- Em seguida no pop-up **'Deploy a model'** preencha os campos seguindo os parametros abaixo:

    - Digite um nome para seu endpoint. Ex.: dataworkshop
    - Apesar de não ser obrigatório o campo descrição recomendo preencher com informações relevantes.
    - Em **'Computer type'** selecione **'ACI'**. Por se tratar de uma demonstração faz mais sentido o ACI, mas se seu modelo for ser consumido por toda empresa o **'AKS'** pode trazer um melhor desempenho.
    - Click em **'Deploy'**

    ![img29](/img/mldeploy1.png)

    - Agora que o deployment terminou já estamos prontos para consumir nosso modelo

    ![img39](/img/mldeploy2.png)
    ___

### Com o deploy do nosso modelo termina esse Workshop. Espero que esse conteúdo te ajude a entender alguns recursos da plataforma de dados do Azure. 

### Caso tenha qualquer dúvida fique a vontade para entrar em contato comigo preferenciamento pelo Linkedin: https://www.linkedin.com/in/fabianojamati/