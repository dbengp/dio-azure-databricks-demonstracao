# dio-azure-databricks-demonstracao
## automatização da ingestão e o processamento de dados usando o Azure Databricks

### Os conceitos e resumo foram retirados da leitura da documentação oficial <https://learn.microsoft.com/pt-br/azure/databricks/> e <https://learn.microsoft.com/pt-br/azure/databricks/dev-tools/cli/>


### Databricks - A Plataforma de Inteligência de Dados.
- O Azure Databricks é uma plataforma central para qualquer organização que busca maximizar o valor de seus dados através de processamento, análise e IA em escala, com foco na qualidade, colaboração e governança. É uma plataforma de análise de dados baseada no Apache Spark, otimizada para o ecossistema Azure. Ele oferece um ambiente unificado e colaborativo para engenharia de dados, ciência de dados, aprendizado de máquina e business intelligence, permitindo que as equipes trabalhem juntas em pipelines de dados e projetos de IA em grande escala. Como o Azure Databricks auxilia na qualidade dos processos de transformação de dados, nesse contexto a qualidade dos processos de transformação de dados é crucial para garantir que as análises e modelos gerados sejam precisos e confiáveis. O Azure Databricks contribui para isso de várias maneiras:
- Arquitetura Lakehouse com Delta Lake:
  * Transacionalidade (ACID): O Delta Lake, a camada de armazenamento subjacente do Databricks, traz capacidades ACID (Atomicidade, Consistência, Isolamento, Durabilidade) para data lakes, o que significa que as transformações de dados são confiáveis. Isso evita corrupção de dados e garante que as operações (como inserções, atualizações e exclusões) sejam completas ou revertidas, mantendo a integridade dos dados.
  * Schema Enforcement e Evolução: O Delta Lake permite a imposição de esquemas, prevenindo a inserção de dados que não se ajustam ao esquema definido, o que é fundamental para a qualidade dos dados. Além disso, ele suporta a evolução do esquema, permitindo que você adapte seus dados conforme as necessidades mudam sem interromper os pipelines existentes.
  * Viagem no Tempo (Time Travel): A capacidade de "viagem no tempo" permite que você acesse versões anteriores dos seus dados. Isso é inestimável para auditoria, reprodução de experimentos, recuperação de erros ou simplesmente para entender como os dados evoluíram ao longo do tempo, contribuindo diretamente para a rastreabilidade e a qualidade.
  * Camadas Bronze, Prata e Ouro (Medallion Architecture): O Databricks incentiva a arquitetura de medalhão (Bronze, Prata, Ouro), onde os dados são incrementalmente refinados.
    * Bronze: Dados brutos e imutáveis.
    * Prata: Dados limpos e filtrados, com transformações básicas aplicadas.
    * Ouro: Dados agregados e preparados para consumo final (BI, ML), garantindo que apenas dados de alta qualidade cheguem aos usuários finais.
- Delta Live Tables (DLT):
  * O DLT simplifica a construção e o gerenciamento de pipelines de ETL confiáveis. Ele oferece qualidades de dados integradas e verificações de validação (expectativas), permitindo definir regras sobre a qualidade dos dados em cada etapa da transformação. Falhas nessas expectativas podem disparar alertas ou interromper o pipeline, garantindo que apenas dados válidos avancem.
  * Automatiza a orquestração e o monitoramento, reduzindo a complexidade e os erros manuais.
- Processamento Distribuído e Escalável (Apache Spark Otimizado):
  * O Databricks é construído sobre o Apache Spark, um motor de processamento distribuído, permitindo lidar com grandes volumes de dados. A capacidade de escalar horizontalmente significa que as transformações podem ser executadas de forma eficiente e rápida, mesmo com conjuntos de dados massivos, o que é crucial para manter a qualidade e a pontualidade dos dados.
  * O motor Photon, otimizado para o Databricks, acelera o desempenho das cargas de trabalho do Spark, resultando em transformações de dados mais rápidas e eficientes.
- Colaboração e Produtividade:
  * Ambiente de notebook colaborativo que permite que engenheiros de dados, cientistas de dados e analistas trabalhem juntos nos mesmos conjuntos de dados e códigos, facilitando a revisão por pares e a consistência das transformações.
  * Suporte a múltiplas linguagens (Python, Scala, SQL, R) oferece flexibilidade para as equipes usarem a linguagem mais adequada para cada tarefa, sem comprometer a qualidade do processo.
- Governança Unificada (Unity Catalog):
  * O Unity Catalog fornece uma camada unificada de governança para todos os ativos de dados e IA (tabelas, arquivos, notebooks, modelos), permitindo definir políticas de acesso e segurança uma única vez e aplicá-las consistentemente. Isso garante que apenas usuários autorizados acessem e modifiquem dados, protegendo a integridade e a qualidade.
  * Oferece linhagem de dados e auditoria, permitindo rastrear a origem e as transformações dos dados, o que é vital para depuração e garantia de qualidade.
- Principais Features do Azure Databricks:
  * Data Lakehouse Platform: Uma arquitetura unificada que combina os melhores aspectos de data lakes (flexibilidade, baixo custo) e data warehouses (estrutura, governança, transacionalidade).
  * Delta Lake: Camada de armazenamento open-source que adiciona confiabilidade, desempenho e governança a data lakes.
  * Apache Spark Otimizado: Versão otimizada do Spark para performance superior, incluindo o motor Photon para consultas rápidas.
  * Workspaces e Notebooks Colaborativos: Ambientes interativos para desenvolvimento de código em diversas linguagens, com recursos de colaboração em tempo real.
  * Databricks Runtime: Conjuntos de bibliotecas e otimizações pré-configuradas para o Spark, garantindo ambientes de execução eficientes.
  * Delta Live Tables (DLT): Ferramenta para construir e gerenciar pipelines de ETL com qualidade de dados e monitoramento integrados.
  * Unity Catalog: Solução de governança unificada para dados e ativos de IA, oferecendo controle de acesso granular e linhagem.
  * Databricks SQL: Um serviço serverless que permite aos analistas de dados executar consultas SQL diretamente nos seus data lakes com alto desempenho.
  * MLflow: Plataforma open-source para gerenciar o ciclo de vida do aprendizado de máquina (rastreamento de experimentos, empacotamento de código, gerenciamento de modelos e registro de modelos).
  * Integração com Azure: Conexão nativa com outros serviços Azure como Azure Data Lake Storage, Azure Data Factory, Azure Synapse Analytics, Power BI e Azure Machine Learning.
  * Jobs e Orquestração: Capacidade de agendar e orquestrar tarefas de processamento de dados e ML, com monitoramento e alertas.
  * Databricks Workflows: Ferramenta para orquestrar pipelines de dados complexos com dependências e lógica condicional entre tarefas.

- Trabalhos Adequados para Uso do Azure Databricks. O Azure Databricks é uma ferramenta poderosa e versátil, adequada para uma ampla gama de trabalhos e cargas de trabalho que envolvem Big Data, análise e IA:
  * Engenharia de Dados (ETL/ELT):
    * Construção de pipelines de dados robustos para ingestão, limpeza, transformação e carregamento de dados em escala, tanto em batch quanto em streaming.
    * Implementação de arquiteturas Lakehouse, transformando dados brutos em formatos otimizados para consumo.
    * Processamento de dados semi-estruturados e não estruturados (logs, dados de sensores, texto).
  * Ciência de Dados e Análise Preditiva:
    * Preparação e engenharia de features para modelos de Machine Learning.
    * Treinamento e validação de modelos de ML em escala, utilizando bibliotecas populares como scikit-learn, TensorFlow e PyTorch.
    * Experimentação de ML com MLflow para rastrear experimentos e gerenciar modelos.
  * Business Intelligence (BI) e Análise Avançada:
    * Habilitação de consultas SQL de alta performance em grandes conjuntos de dados para análises exploratórias e geração de relatórios.
    * Criação de dashboards e visualizações conectadas diretamente aos dados processados no Databricks.
    * Análises ad-hoc e descoberta de insights em tempo real ou quase real.
  * Streaming de Dados em Tempo Real:
    * Processamento de dados de streaming de fontes como Kafka, Azure Event Hubs ou Azure IoT Hub para análises em tempo real e detecção de anomalias.
    * Construção de aplicações de streaming para monitoramento contínuo e tomada de decisões em tempo real.
  * Machine Learning Operations (MLOps):
    * Automação do ciclo de vida de ML, desde o desenvolvimento e treinamento até a implantação e monitoramento de modelos em produção.
    * Gerenciamento de versões de modelos e colaboração entre equipes de ciência de dados e engenharia.
  * Data Warehousing Moderno:
    * Substituição ou complemento de data warehouses tradicionais com a arquitetura lakehouse, oferecendo maior flexibilidade e escalabilidade.
    * Execução de cargas de trabalho analíticas complexas com desempenho otimizado.
  * Casos de Uso de IA Generativa (GenAI):
    * Engenharia de features e ajuste fino de Large Language Models (LLMs).
    * Construção de aplicações de IA Generativa que consomem dados de alta qualidade do lakehouse.

### Demonstração de uma solução de ingestão de dados com Azure Databricks - via CLI
- Preparação (Autenticação e Extensão Databricks): Primeiro, você precisará se autenticar no Azure e instalar a extensão Databricks para a CLI do Azure.
```
az login
az extension add --name databricks
```
- Para gerenciar notebooks você usará os comandos `az databricks notebook`. Você pode criar um arquivo local (.py, .scala, .sql, ou .ipynb) com o código do seu notebook e importa para o Databricks.
```
az databricks notebook import --path /Users/YourUsername/DataProcessing --language PYTHON --format SOURCE --content @/path/to/your/data_processing_notebook.py --workspace-url https://<your-databricks-workspace-url>
```
- Para executar um NotebookEmbora usa-se células, porém em um fluxo CLI a execução geralmente é feita via Jobs. No entanto, você pode usar a API de runs para executar um notebook.
- Para gerenciamento de Jobs que executam seus notebooks, você usará os comandos `az databricks job`
```
az databricks job create --name "Data Processing Job" \
    --tasks '[{"task_key": "ProcessData", "notebook_task": {"notebook_path": "/Users/YourUsername/DataProcessing", "base_parameters": {}}, "new_cluster": {"spark_version": "12.2.x-scala2.12", "node_type_id": "Standard_DS3_v2", "num_workers": 2}}]' \
    --workspace-url https://<your-databricks-workspace-url>
```
- Executar um Job:
```
az databricks job run --job-id <your-job-id> --workspace-url https://<your-databricks-workspace-url>
```
- Listar Jobs:
```
az databricks job list --workspace-url https://<your-databricks-workspace-url>
```
- Obter o status de uma execução de Job:
```
az databricks run get --run-id <your-run-id> --workspace-url https://<your-databricks-workspace-url>
```
