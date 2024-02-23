## Explorando o Machine Learning Automatizado no Azure Machine Learning

Nesse repositório será demonstrado um passo a passo para a utilização do Azure Machine Learning, realizando a configuração de um modelo, conjunto de dados, teste do modelo e apresentação dos resultados. 

#### Pré-requisitos
---
Temos como pré-requisito a criação uma conta gratuita na Azure ou disponibilidade de créditos para uso.

### Tutorial
---
#### Criando um recurso
---
O primeiro passo é fazer a criação de um recurso no [Portal Azure](https://portal.azure.com/), logo na página principal já temos um botão destinado a criação do recurso.

![Criando um recurso](https://i.imgur.com/mAcyJQE.png)

Após clicar nesse botão, será redirecionado para a seguinte página:

![Página de criação do recurso](https://i.imgur.com/VJa05Fn.png)

Para facilitar, clique em **Análises**,selecione **Azure Machine Learning** e clique em **Criar**.
>Observação: Você também pode pesquisar diretamente por Azure Machine Learning no search

Após clicar em Criar, será aberta uma página para preenchimento das informações, onde será necessário inserir as informações conforme o exemplo abaixo:

```yaml
    Assinatura: sua assinatura do Azure .
    Grupo de recursos: Crie ou selecione um grupo de recursos .
    Nome: Insira um nome exclusivo para seu espaço de trabalho .
    Região: Selecione a região geográfica mais próxima .
    Conta de armazenamento: observe a nova conta de armazenamento padrão que será criada para seu espaço de trabalho .
    Cofre de chaves: Observe o novo cofre de chaves padrão que será criado para seu espaço de trabalho .
    Insights de aplicativo: observe o novo recurso padrão de insights de aplicativo que será criado para seu espaço de trabalho .
    Registro de contêiner: Nenhum ( um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner ).
```



#### Acessando o recurso
---
Depois de criado, podemos acessar o recurso criado através do [Portal Azure](https://portal.azure.com/):

![Página de criação do recurso](https://i.imgur.com/n31UqPJ.png)

Será necessário clicar no nome do nosso recurso e depois clicar no botão central **Iniciar o estúdio** ou entrar no [Estúdio de Aprendizado de Máquina](https://ml.azure.com/).

Na imagem abaixo podemos ver a página principal e também as principais guias que utilizaremos para cumprir o objetivo, em suas respectivas ordens.

![Pagina Principal do Estúdio](https://i.imgur.com/5KRdiRa.png)

##### 1° Execução: Criar o modelo automatizado
---
Clique em ML Automatizado e insira as seguintes configurações.
Em configurações básicas:

````yaml
Nome do trabalho: mslearn-bike-automl
Novo nome do experimento: mslearn-bike-rental
Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
Marcadores: nenhum
````

Em Tipo de tarefa e dados selecione **Regressão**, clique em **criar**. Na aba Tipo de dados, insira:
```yaml
Nome: aluguel de bicicletas
Descrição: dados históricos de aluguel de bicicletas
Tipo: Tabular
```
Em Fonte de dados, selecione **arquivos da web** e informe a URL https://aka.ms/bike-rentals e não selecione o campo **Ignorar validação de dados**.

Em configurações selecione cada um dos campos:
``` yml
Formato de arquivo: Delimitado
Delimitador: Vírgula
Codificação: UTF-8
Cabeçalhos de coluna: apenas o primeiro arquivo possui cabeçalhos
Pular linhas: Nenhum
O conjunto de dados contém dados multilinhas : não selecione
Esquema: Incluir todas as colunas exceto Caminho
```
##### 2° Execução: Verificar o job
---
Após criar o modelo automatizado e ele ser executado com sucesso, podemos ver na aba **Jobs** seu _status_ e também o melhor modelo definido.

![Tarefa executada](https://i.imgur.com/J9n45Op.png)

Clicando no **nome do algoritmo**, seremos direcionados para a página do modelo, onde poderemos implantar o modelo treinado:

![Implantando](https://i.imgur.com/KKFD7ey.png)

Se entrarmos na aba **Modelos**, poderemos ver esse modelo que implantamos.

##### 3° Execução: Testar o modelo
---
Na aba Pontos de extremidade, é possível ver nosso _endpoint_ e verificar se ele já está executando com sucesso, para isso checamos os seguintes pontos. Se estiver com _status_ de _running_, será necessário aguardar até ficar como _succeeded_, caso contrário não será possível testar o modelo.

![Status](https://i.imgur.com/eGZzCHu.png)

Por fim, para testar o modelo, basta clicar na aba **Testar**. Inserindo o seguinte json:
```json
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```

O resultado será:
![Testando modelo](https://i.imgur.com/28qPBSq.png)

