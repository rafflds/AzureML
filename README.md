🚀 Explorando o Machine Learning Automatizado no Azure Machine Learning
<p align="center">
<img src="https://azurecomcdn.azureedge.net/cvt-d2037a36a6656f984528a551e9101a640426c329b133732a87217e5b334a03c2/images/page/services/machine-learning/azure-machine-learning-icon.png" alt="Ícone do Azure Machine Learning" width="150">
</p>


🛠️ Pré-requisitos
Uma assinatura do Azure ativa.

Acesso ao portal do Azure.



⚙️ Passo a Passo
Criar um Workspace do Azure Machine Learning

Acesse o portal do Azure: https://portal.azure.com

Crie um novo recurso do tipo "Machine Learning".

Preencha as configurações conforme abaixo:

Assinatura: Sua assinatura do Azure.

Grupo de recursos: Crie um novo ou selecione um existente.

Nome: Escolha um nome único para o seu workspace.

Região: Leste dos EUA.

Conta de armazenamento, Cofre de chaves e Insights do aplicativo: Observe os padrões que serão criados.

Registro de contêiner: Deixe como "Nenhum".

Aguarde a criação e vá para o recurso.

No "Grupo de Recursos", atualize as permissões, adicione a role "Administrador do Azure AI" e seu email como membro.

Retorne para o seu workspace.

Lançar o Azure Machine Learning Studio

No seu workspace, clique em "Launch studio" ou acesse: https://ml.azure.com

Selecione seu workspace caso necessário.

Usar Machine Learning Automatizado para Treinar um Modelo

Navegue até a página "ML Automatizado" (em "Criação").

Crie um novo trabalho com as seguintes configurações:

Nome do trabalho: Mantenha o padrão.

Novo nome do experimento: mslearn-bike-rental

Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas

Tipo de tarefa: Regressão

Conjunto de dados: Crie um novo com as seguintes opções:

Nome: bike-rentals

Descrição: Historic bike rental data

Tipo: Tabela (mltable)

Fonte de dados: De arquivos locais

Tipo de armazenamento de dados: Azure Blob Storage

Nome: workspaceblobstore

Pasta de upload: Baixe e descompacte https://aka.ms/bike-rentals e envie os arquivos.

Coluna de destino: alugueis (inteiro)

Métrica primária: NormalizedRootMeanSquaredError

Modelos permitidos: RandomForest e LightGBM

Limites:

Máximo de ensaios: 3

Máximo de ensaios simultâneos: 3

Máximo de nós: 3

Limite de pontuação métrica: 0.085

Tempo limite do experimento: 15

Tempo limite de iteração: 15

Habilitar rescisão antecipada: Selecionado

Validação: Divisão de validação de trem, com 10% de dados para validação.

Cálculo:

Tipo de computação: Sem servidor

Tipo de máquina virtual: CPU

Camada de máquina virtual: Dedicada

Tamanho da máquina virtual: Standard_DS3_V2 (ou outro disponível).

Número de instâncias: 1

Envie o trabalho e aguarde a conclusão. ☕

Avaliar o Melhor Modelo

Na guia "Visão geral" do trabalho, visualize o melhor modelo.

Clique no nome do algoritmo do melhor modelo.

Na guia "Métricas", visualize os gráficos de resíduos e prediction_true.

Implantar e Testar o Modelo

Na guia "Modelo", selecione "Implantar" -> "Ponto de extremidade em tempo real".

Use as seguintes configurações:

Máquina virtual: Standard_DS3_v2

Contagem de instâncias: 3

Ponto final: Novo

Nome do ponto de extremidade: Deixe o padrão.

Nome da implantação: Deixe o padrão.

Inferência de coleta de dados: Desativado

Modelo de pacote: Desativado

Aguarde a implantação e depois navegue para "Endpoints" (menu à esquerda).

Abra o endpoint criado.

Na guia "Teste", substitua o JSON do modelo pelo seguinte:

{
    "input_data": {
        "columns": [
        "day",
        "mnth",
        "year",
        "season",
        "holiday",
        "weekday",
        "workingday",
        "weathersit",
        "temp",
        "atemp",
        "hum",
        "windspeed"
        ],
        "index": [0],
        "data": [[1,1,2022,2,0,1,1,2,0.3,0.3,0.3,0.3]]
    }
}
Use code with caution.
Json
Clique em "Testar" e veja o resultado.

Limpar

Na guia "Endpoints", selecione o endpoint e clique em "Excluir".

No portal do Azure, exclua o "Grupo de recursos" do Azure Machine Learning.

🏆 Conclusão
Parabéns! Você acabou de explorar o poder do Machine Learning Automatizado no Azure Machine Learning. Você aprendeu como criar um workspace, treinar e avaliar um modelo, implantá-lo como um serviço web e testá-lo com dados reais. Agora você está um passo mais perto de construir soluções de inteligência artificial que podem transformar seu negócio!

🔗 Links Úteis
Documentação do Azure Machine Learning

Tutorial de Machine Learning Automatizado

Download dos dados de aluguel de bicicletas
