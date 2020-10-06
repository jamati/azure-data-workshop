# Gerar dados simulados para serem consumidos pelo Event Hub

> 1. Agora vamos simular dados entrando no nosso Event Hub 

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

## Próximo passo
___

[Criar nossa dashboard no PBI para visualizar nossos dados em stream](./dashboard_pbi.md)