# Laboratorio-IA900

### Aprendizado de Máquina Automatizado no Azure

- Documentação utilizada para executar esse processo:
- https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html

### 1 - Entre no portal do Azure "https://portal.azure.com" usando suas credenciais da Microsoft.

### 2 - Selecione "+Criar" um recurso, procure Aprendizado de Máquina e crie um novo recurso de Aprendizado de Máquina do Azure com as seguintes configurações:

- Assinatura: sua assinatura do Azure.
- Grupo de recursos: crie ou selecione um grupo de recursos.
- Nome: insira um nome exclusivo para seu espaço de trabalho.
- Região: Selecione a região geográfica mais próxima.
- Conta de armazenamento: observe a nova conta de armazenamento padrão que será criada para seu espaço de trabalho.
- Cofre de chaves: observe o novo cofre de chaves padrão que será criado para seu espaço de trabalho.
- Application insights: observe o novo recurso padrão de insights de aplicativo que será criado para seu espaço de trabalho.
- Registro de contêiner: Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).

### 3 - Selecione Revisar "+criar" e, em seguida, selecione "Criar". Aguarde até que seu espaço de trabalho seja criado (pode levar alguns minutos) e vá para o recurso implantado.

### 4 - Selecione Iniciar estúdio (ou abra uma nova guia do navegador e navegue até "https://ml.azure.com" e entre no estúdio do Aprendizado de Máquina do Azure usando sua conta da Microsoft). Feche todas as mensagens exibidas.

### 5 - No estúdio de Aprendizado de Máquina do Azure, você deve ver seu espaço de trabalho recém-criado. Caso contrário, selecione Todos os espaços de trabalho no menu à esquerda e, em seguida, selecione o espaço de trabalho que você acabou de criar.

## Usar o aprendizado de máquina automatizado para treinar um modelo

### 1- No estúdio de Aprendizado de Máquina do Azure, exiba a página ML automatizada (em Criação).

### 2- Crie um novo trabalho de ML automatizado com as seguintes configurações, usando Avançar conforme necessário para progredir pela interface do usuário:

Configurações básicas:
- Nome do trabalho: mslearn-bike-automl
- Novo nome do experimento: mslearn-bike-rental
- Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- Tags: nenhuma
 
Tipo de tarefa & data:
- Selecionar tipo de tarefa: Regressão
- Selecionar conjunto de dados: crie um novo conjunto de dados com as seguintes configurações:

Tipo de dados:
- Nome: bike-rentals
- Descrição: Dados históricos de aluguer de bicicletas
- Tipo: Tabular

Fonte de dados:
- Selecionar de arquivos da Web
- URL da Web: https://aka.ms/bike-rentals
- Ignorar validação de dados: não selecione

Configurações:
- Formato de arquivo: Delimitado
- Delimitador: Vírgula
- Codificação: UTF-8
- Cabeçalhos de coluna: Somente o primeiro arquivo tem cabeçalhos
- Pular linhas: Nenhum
- O conjunto de dados contém dados de várias linhas: não selecione

Esquema:
- Incluir todas as colunas diferentes de Caminho
- Revisar os tipos detectados automaticamente

Selecione Criar. Depois que o conjunto de dados for criado, selecione o conjunto de dados de aluguel de bicicletas para continuar a enviar o trabalho de ML automatizado.

Configurações da tarefa:
- Tipo de tarefa: Regressão
- Conjunto de dados: aluguel de bicicletas
- Coluna de destino: Aluguéis (inteiro)

Definições de configuração adicionais:
- Métrica primária: Erro quadrático médio da raiz normalizada
- Explicar melhor modelo: Não selecionado
- Use todos os modelos suportados: Nãoselecionado. Você restringirá o trabalho para tentar apenas alguns algoritmos específicos.
- Modelos permitidos: selecione apenas RandomForest e LightGBM — normalmente você gostaria de tentar o maior número possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.

Limites: expanda esta seção
- Máximo de tentativas: 3
- Máximo de tentativas simultâneas: 3
- Nós máximos: 3
- Limiar de pontuação métrica: 0,085 (de modo que, se um modelo atingir uma pontuação métrica quadrática média normalizada de 0,085 ou menos, o trabalho termina.)
- Tempo limite: 15
- Tempo limite de iteração: 15
- Habilitar rescisão antecipada: Selecionado

Validação e teste:
- Tipo de validação: Divisão de validação de trem
- Porcentagem de dados de validação: 10
- Conjunto de dados de teste: Nenhum

Computação:
- Selecione o tipo de computação: Serverless
- Tipo de máquina virtual: CPU
- Camada de máquina virtual: Dedicado
- Tamanho da máquina virtual: Standard_DS3_V2*
- Número de instâncias: 1

### 3 - Envie o trabalho de treinamento. Ele começa automaticamente.

### 4 - Aguarde a conclusão do trabalho. Pode demorar um pouco – agora pode ser um bom momento para uma pausa para o café!

## Reveja o melhor modelo

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo treinado.

### 1 - Na guia Visão geral do trabalho de aprendizado de máquina automatizado, observe o melhor resumo do modelo.

### 2 - Em Melhor resumo de modelo, selecione o texto em Nome do algoritmo para o melhor modelo para exibir seus detalhes.
![image](https://github.com/XlfelipeX/Laboratorio-IA900/assets/144381176/cc20cf03-1678-4488-8549-5968c2dc1106)

### 3 - Selecione a guia Métricas e selecione os gráficos de resíduos e predicted_true se ainda não estiverem selecionados.

### 4 - Analise os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre os valores previstos e reais) como um histograma. O gráfico predicted_true compara os valores previstos com os valores verdadeiros.
![image](https://github.com/XlfelipeX/Laboratorio-IA900/assets/144381176/29d0282b-75fa-4aab-9113-458150774239)

## Implantar e testar o modelo

### 1 - Na guia Modelo para obter o melhor modelo treinado pelo seu trabalho de aprendizado de máquina automatizado, selecione Implantar e usar a opção Serviço Web para implantar o modelo com as seguintes configurações:
![Captura de tela 2024-02-04 124015](https://github.com/XlfelipeX/Laboratorio-IA900/assets/144381176/d92a2072-0b2d-484d-85e3-b2cb13658b53)
- Nome: aluguéis de previsão
- Descrição: Prever aluguéis de ciclos
- Tipo de computação: Instância de Contêiner do Azure
- Habilitar autenticação: Selecionado

### 2 - Aguarde o início da implantação - isso pode levar alguns segundos. O status de implantação para o ponto de extremidade de aluguel de previsão será indicado na parte principal da página como Em execução.

### 3 - Aguarde até que o status Implantar seja alterado para Bem-sucedido. Isso pode levar de 5 a 10 minutos.

## Testar o serviço implantado
Agora você pode testar seu serviço implantado.

### 1 - No estúdio do Aprendizado de Máquina do Azure, no menu à esquerda, selecione Pontos de extremidade e abra o ponto de extremidade em tempo real de aluguéis de previsão.

### 2 - Na página de ponto de extremidade em tempo real de aluguéis de previsão, exiba a guia Teste.

### 3 - No painel Dados de entrada para testar o ponto de extremidade, substitua o modelo JSON pelos seguintes dados de entrada:
https://github.com/XlfelipeX/Laboratorio-IA900/blob/main/JSON

### 4 - Clique no botão Testar.

### 5 - Analise os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada - semelhante a este:
![image](https://github.com/XlfelipeX/Laboratorio-IA900/assets/144381176/ee455102-8067-46af-a8db-51c0218b0587)

O painel de teste pegou os dados de entrada e usou o modelo treinado para retornar o número previsto de aluguéis.

Vamos rever o que você fez. Você usou um conjunto de dados de dados históricos de aluguel de bicicletas para treinar um modelo. O modelo prevê o número de aluguéis de bicicletas esperados em um determinado dia, com base em características sazonais e meteorológicas.
