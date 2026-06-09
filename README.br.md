[![Português](https://img.shields.io/badge/lang-PT--BR-green)](README.br.md)
[![English](https://img.shields.io/badge/lang-EN-white)](README.md)

# Plantas do Brasil

Pipeline de Engenharia de Dados e Ciência de Dados aplicado a registros de biodiversidade da flora brasileira. Este projeto surgiu da vontade de aplicar, na prática, conceitos de engenharia de dados, análise exploratória e machine learning em um contexto real. A ideia era ir além de exemplos prontos e trabalhar com um tema que me desperta interesse, utilizando dados públicos e construindo uma visualização que qualquer pessoa pudesse explorar e compreender.

Os dados foram obtidos no [GBIF](https://www.gbif.org/) *(Global Biodiversity Information Facility)*, uma das maiores bases de biodiversidade do mundo, com bilhões de registros de ocorrência de espécies disponibilizados gratuitamente por instituições, pesquisadores e iniciativas de ciência cidadã.
 
### Estrutura do pipeline

```
Plantas-do-Brasil/
├── pipeline.ipynb      # coleta, limpeza e armazenamento
├── analise.ipynb              # EDA + Clustering K-Means
├── geovisualizacao.ipynb      # mapa interativo com Folium
├── dados/
│   ├── plantas_brasil.parquet  
│   └── plantas_brasil.csv   
├── extra/ 
│   ├── BR_UF_2025   
│   └── images.png    
└── mapa_plantas_brasil.html    
```

# Etapas

**Etapa 1 - Engenharia de Dados:** `pipeline.ipynb`

Coleta dados de plantas nativas do Brasil por meio da API REST do GBIF, realiza a limpeza dos registros e os armazena em formatos otimizados para análise. O que acontece aqui:

- Requisições paginadas à API (300 registros/página) com tratamento de erros e pausa entre chamadas;
- Seleção e renomeação de colunas relevantes;
- Remoção de registros sem coordenadas, normalização de texto, validação espacial do território brasileiro;
- Remoção de registros duplicados por `gbifID`;
- Armazenamento em `.parquet` e `.csv`.

**Etapa 2 - EDA + Machine Learning:** `analise.ipynb`

Análise exploratória dos dados coletados e agrupamento geográfico via K-Means. O que foi feito: 

- Top 10 espécies com mais registros; 
- Top 10 estados com mais registros; 
- Distribuição por tipo de fonte.

K-Means para agrupar coordenadas geográficas em regiões com perfis similares de biodiversidade. O que foi feito:

- Método do Cotovelo + Silhouette Score para escolha do K;
- Scatter plot lat/long colorido por cluster;
- Espécie top, estado top e centroide por cluster.

**Etapa 3 - Mapa Interativo:** `geovisualizacao.ipynb`  

Mapa construído com [Folium](https://python-visualization.github.io/folium/) (wrapper Python para Leaflet.js).

- Mapa de calor (Heatmap): visualização da densidade de registros em todo o território brasileiro;
- Marcadores interativos: até 2.000 pontos exibidos individualmente, com informações detalhadas em pop-up;
- Clusters A–E: ativação e desativação independente de cada agrupamento gerado pelo K-Means;
- MiniMapa: visão geral para facilitar a navegação pelo mapa;
- Tela cheia: botão para expandir a visualização em modo fullscreen.

Cada marcador apresenta informações sobre a espécie, família botânica, estado, município, ano do registro e cluster ao qual pertence.

# Exemplos

- Top 10 Espécies com Mais Registros:

<img src="extra/top 10 especies.png" width="500">

- Escolha do K para o K-Means:

<img src="extra/k means.png" width="500">

- Mapa gerado com Folium:

<img src="extra/mapa.png" width="500">

<br>

# Como rodar

1. Clone o repositorio

```bash
git clone https://github.com/seu-usuario/Plantas-do-Brasil.git
cd Plantas-do-Brasil
```

2. Instale as dependencias

```bash
pip install -r requirements.txt
```

3. Execute os notebooks em ordem

Abra o Jupyter e rode cada notebook na sequencia:

```
pipeline.ipynb 
analise.ipynb
geovisualizacao.ipynb
```

# Ferramentas Utilizadas

- `requests`: consumo da API REST do GBIF.
- `pandas` e `pyarrow`: processamento e armazenamento dos dados.
- `matplotlib` e `seaborn`: análise exploratória e visualizações.
- `scikit-learn`: agrupamento geográfico com K-Means.
- `folium`: construção do mapa interativo.




