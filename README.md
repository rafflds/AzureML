# 🚀 Explorando o Machine Learning Automatizado no Azure Machine Learning

<p align="center">
<img src="https://azurecomcdn.azureedge.net/cvt-d2037a36a6656f984528a551e9101a640426c329b133732a87217e5b334a03c2/images/page/services/machine-learning/azure-machine-learning-icon.png" alt="Ícone do Azure Machine Learning">
</p>

## Tabela de Conteúdos
- [Pré-requisitos](#pré-requisitos)
- [Passo a Passo](#passo-a-passo)
  - [Criar um Workspace do Azure Machine Learning](#criar-um-workspace-do-azure-machine-learning)
  - [Lançar o Azure Machine Learning Studio](#lançar-o-azure-machine-learning-studio)
  - [Usar Machine Learning Automatizado para Treinar um Modelo](#usar-machine-learning-automatizado-para-treinar-um-modelo)
  - [Avaliar o Melhor Modelo](#avaliar-o-melhor-modelo)
  - [Implantar e Testar o Modelo](#implantar-e-testar-o-modelo)
  - [Limpar](#limpar)
- [Conclusão](#conclusão)
- [Links Úteis](#links-úteis)
- [Contribuição](#contribuição)
- [Suporte](#suporte)

## 🛠️ Pré-requisitos
- Uma assinatura do Azure ativa.
- Acesso ao portal do Azure.

## ⚙️ Passo a Passo

### Criar um Workspace do Azure Machine Learning
1. Acesse o portal do Azure: [https://portal.azure.com](https://portal.azure.com)
2. Crie um novo recurso do tipo "Machine Learning".
3. Preencha as configurações conforme abaixo:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie um novo ou selecione um existente.
   - **Nome**: Escolha um nome único para o seu workspace.
   - **Região**: Leste dos EUA.
   - **Conta de armazenamento, Cofre de chaves e Insights do aplicativo**: Observe os padrões que serão criados.
   - **Registro de contêiner**: Deixe como "Nenhum".
4. Aguarde a criação e vá para o recurso.
5. No "Grupo de Recursos", atualize as permissões, adicione a role "Administrador do Azure AI" e seu email como membro.
6. Retorne para o seu workspace.

### Lançar o Azure Machine Learning Studio
1. No seu workspace, clique em "Launch studio" ou acesse: [https://ml.azure.com](https://ml.azure.com)
2. Selecione seu workspace caso necessário.

### Usar Machine Learning Automatizado para Treinar um Modelo
1. Navegue até a página "ML Automatizado" (em "Criação").
2. Crie um novo trabalho com as seguintes configurações:
   - **Nome do trabalho**: Mantenha o padrão.
   - **Novo nome do experimento**: mslearn-bike-rental
   - **Descrição**: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
   - **Tipo de tarefa**: Regressão
3. Conjunto de dados:
   - **Nome**: bike-rentals
   - **Descrição**: Historic bike rental data
   - **Tipo**: Tabela (mltable)
   - **Fonte de dados**: De arquivos locais
   - **Tipo de armazenamento de dados**: Azure Blob Storage
   - **Nome**: workspaceblobstore
   - **Pasta de upload**: Baixe e descompacte [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals) e envie os arquivos.
   - **Coluna de destino**: alugueis (inteiro)
4. Configurações do experimento:
   - **Métrica primária**: NormalizedRootMeanSquaredError
   - **Modelos permitidos**: RandomForest e LightGBM
   - **Limites**:
     - Máximo de ensaios: 3
     - Máximo de ensaios simultâneos: 3
     - Máximo de nós: 3
     - Limite de pontuação métrica: 0.085
     - Tempo limite do experimento: 15
     - Tempo limite de iteração: 15
     - Habilitar rescisão antecipada: Selecionado
     - Validação: Divisão de validação de trem, com 10% de dados para validação.
5. Cálculo:
   - **Tipo de computação**: Sem servidor
   - **Tipo de máquina virtual**: CPU
   - **Camada de máquina virtual**: Dedicada
   - **Tamanho da máquina virtual**: Standard_DS3_V2 (ou outro disponível)
   - **Número de instâncias**: 1
6. Envie o trabalho e aguarde a conclusão. ☕

### Avaliar o Melhor Modelo
1. Na guia "Visão geral" do trabalho, visualize o melhor modelo.
2. Clique no nome do algoritmo do melhor modelo.
3. Na guia "Métricas", visualize os gráficos de resíduos e prediction_true.

### Implantar e Testar o Modelo
1. Na guia "Modelo", selecione "Implantar" -> "Ponto de extremidade em tempo real".
2. Use as seguintes configurações:
   - **Máquina virtual**: Standard_DS3_v2
   - **Contagem de instâncias**: 3
   - **Ponto final**: Novo
   - **Nome do ponto de extremidade**: Deixe o padrão.
   - **Nome da implantação**: Deixe o padrão.
   - **Inferência de coleta de dados**: Desativado
   - **Modelo de pacote**: Desativado
3. Aguarde a implantação e depois navegue para "Endpoints" (menu à esquerda).
4. Abra o endpoint criado.
5. Na guia "Teste", substitua o JSON do modelo pelo seguinte:
```json
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
