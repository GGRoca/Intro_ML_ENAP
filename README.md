Este repositório contém uma pipeline completa de processamento de dados e machine learning voltada para a análise e segmentação do mercado de exibição cinematográfica brasileiro. O objetivo central é identificar perfis distintos de complexos cinematográficos, avaliando padrões de universalização do acesso e diversificação de programação, conforme as diretrizes do Art. 6º da Lei da ANCINE.
Abaixo está o detalhamento do processo dividido por notebooks:

--------------------------------------------------------------------------------
1. Preparação e Limpeza de Dados (Notebooks A & 0)
O processo inicia-se com a gestão de grandes volumes de dados de bilheteria diária (2023-2025):
• Notebook A: Realiza a pré-leitura de arquivos CSV massivos (mais de 12 milhões de linhas), reduzindo o dataset para colunas essenciais e convertendo-o para o formato Parquet, otimizando o espaço em disco em mais de 85%.
• Notebook 0: Consolida os dados de sessões, integrando-os com informações de salas da ANCINE e dados socioeconômicos do IBGE (PIB e população) via API. Define regras de negócio como a criação de títulos unificados e o cálculo de semanas cinematográficas.
2. Enriquecimento de Obras (Notebook 0.5)
Este notebook foca em construir uma base auxiliar de obras enriquecida:
• Cruza os dados com registros abertos da ANCINE para identificar o nível de produtoras brasileiras e o porte de distribuidoras.
• Identifica distribuidoras "Majors" (como Disney, Warner, Universal) e calcula o porte das demais com base no volume histórico de lançamentos.
3. Análise Exploratória Avançada - EDA (Notebook 1)
Realiza um diagnóstico profundo do mercado para subsidiar a engenharia de atributos:
• Analisa a concentração de público (onde os 5% principais filmes geram 85% do público total).
• Identifica padrões temporais e geográficos, como a maior presença de filmes legendados em grandes capitais.
• Valida a existência de um perfil de "Cinema de Arte", caracterizado por alta diversidade de nacionalidades e uso de distribuidoras independentes.
4. Engenharia de Atributos por Complexo (Notebook 2)
Transforma os dados de milhões de sessões em uma base estruturada por REGISTRO_COMPLEXO:
• Cria mais de 50 features, incluindo métricas de volume, diversidade geográfica (cinema mundial), entropia de programação e flags de natureza jurídica.
• Identifica "cinemas curadores" através de métricas de obras exclusivas e obras de ultranicho.
5. Pré-processamento (Notebook 3)
Prepara a matriz final para os algoritmos de clusterização:
• Resolve problemas de multicolinearidade através da análise do Fator de Inflação da Variância (VIF).
• Cria features compostas de alto valor semântico, como o score de curadoria e o perfil independente.
• Aplica normalização híbrida (StandardScaler e RobustScaler) para lidar com outliers legítimos do mercado.
6. Clusterização e Refinamento (Notebooks 4 & 4.1)
A etapa final de modelagem divide os complexos em grupos comportamentais:
• Notebook 4: Explora modelos de K-Means, definindo k=6 como a segmentação ideal para equilibrar estatística e interpretabilidade, gerando rótulos como "Mainstream Interior" e "Cinemas Públicos Especiais".
• Notebook 4.1: Refina o modelo utilizando HDBSCAN para identificar clusters baseados em densidade, isolando grupos institucionais como o SPCine.
• Explicabilidade: Implementa a tecnologia SHAP para explicar, de forma transparente, quais atributos (como entropia de nacionalidade ou sessões especiais) definem a alocação de um complexo em determinado cluster.
