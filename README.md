# Suicide Data Analysis + Databricks (Bronze → Silver → Gold + Lakeview)

Projeto de engenharia de dados no **Databricks** para coletar, tratar e analisar dados globais de suicídio, correlacionando com IDH, uso de drogas e fatores socioeconômicos, com visualização no **Lakeview**.

## 📦 Estrutura do repositório

### Notebooks de Ingestão (Bronze)
- `scr/WHO - Índice de Suicídio/Bronze.ipynb` — ingestão de dados da WHO GHO API (SDG 3.4.2)
- `scr/World Bank - IDH/Bronze.ipynb` — ingestão do Human Development Index (OWID)
- `scr/WHO - Uso de Drogas/Bronzes.ipynb` — 20 indicadores de drogas da WHO GHO API

### Notebooks de Transformação (Silver)
- `scr/WHO - Índice de Suicídio/Silver.ipynb` — normalização e padronização de dados de suicídio
- `scr/World Bank - IDH/Silver.ipynb` — limpeza e padronização do HDI
- `scr/WHO - Uso de Drogas/Silvers.ipynb` — consolidação de indicadores de drogas (formato long + wide)

### Notebooks de Modelagem (Gold)
- `scr/WHO - Uso de Drogas/Golds.ipynb` — criação de 7 tabelas analíticas Gold
- `scr/WHO - Uso de Drogas/Insights.ipynb` — queries SQL para análise exploratória

### Validação e Documentação
- `scr/Validações/Validações.ipynb` — validação de qualidade e integridade dos dados
- `Ideia e fontes.ipynb` — documentação das fontes de dados e APIs utilizadas
- `Suicide.lvdash.json` — export do dashboard Lakeview

## 📊 Dashboard (Lakeview)

O dashboard apresenta 5 visualizações principais para análise do fenômeno global de suicídio:

### 1. Benchmark do Brasil (2000-Presente)
![Benchmark do Brasil](scr/Validações/Graficos/Benchmark%20do%20Brasil%20%282000-Presente%29.png)
*Comparação da taxa de suicídio do Brasil com EUA, média das Américas, média global e BRICS ao longo do tempo*

### 2. Taxa Média Global de Suicídio
![Taxa Global](scr/Validações/Graficos/Taxa%20Média%20Global%20de%20Suicídio%20%282000-Presente%29.png)
*Tendência histórica da taxa média global: o problema está melhorando ou piorando?*

### 3. Suicídio vs. Tratamento de Drogas
![Correlação Drogas](scr/Validações/Graficos/Suicídio%20vs.%20Tratamento%20de%20Drogas.png)
*Scatter plot mostrando a correlação entre cobertura de tratamento de drogas e taxas de suicídio*

### 4. Disparidade de Gênero
![Disparidade Gênero](scr/Validações/Graficos/Disparidade%20de%20Gênero%20%28O%20_Quem_%29.png)
*Top 10 países com maior razão homem/mulher nas taxas de suicídio*

### 5. Hotspots de Risco
![Hotspots](scr/Validações/Graficos/Hotspots%20de%20Risco%20%28O_Onde_%29.png)
*Mapa global destacando países com aumentos significativos recentes (>20% em 1 ano)*

---

## 🔎 Visão Geral das Camadas

### Bronze (Ingestão Bruta)
- **WHO Suicide Data**: Taxas de suicídio por país/ano/sexo (2000-2024)
- **HDI (OWID)**: Índice de Desenvolvimento Humano por país/ano
- **WHO Drug Indicators**: 20 indicadores sobre uso de drogas, tratamento e prevenção

### Silver (Normalização)
- Padronização de códigos de país (ISO3)
- Mapeamento de dimensões (sexo, região)
- Limpeza de dados inválidos e duplicados
- Criação de formato long (drug_indicators) e wide (drug_indicators_wide)

### Gold (Modelagem Analítica)
7 tabelas otimizadas para análise:

1. **suicide_hdi_analysis**: Análise temporal correlacionando suicídio x HDI
2. **gender_disparity_analysis**: Comparação entre taxas masculinas e femininas
3. **country_rankings**: Rankings global e regional por ano
4. **global_metrics**: Métricas agregadas (média, máximo, mínimo, desvio)
5. **significant_changes_alerts**: Alertas de mudanças >20% (1 ano) ou >50% (5 anos)
6. **momentum_analysis**: Velocidade e aceleração das mudanças
7. **multifactor_correlation**: Correlação entre suicídio, HDI e tratamento de drogas

---

## 📈 Insights Principais

### 🌍 Cenário Global
- A taxa global média de suicídio apresenta tendências de melhoria ou piora dependendo da região e período analisado
- Existem diferenças regionais significativas, com algumas regiões mostrando padrões distintos ao longo do tempo

### 🇧🇷 Brasil em Destaque
- O Brasil pode ser comparado com países BRICS, América Latina, média global e economias desenvolvidas como os EUA para entender sua posição relativa
- A análise de tendências permite identificar se o Brasil está melhorando ou piorando em relação aos seus pares

### 👥 Disparidade de Gênero
- Países apresentam diferentes níveis de disparidade entre taxas masculinas e femininas, com alguns mostrando razões muito elevadas
- A análise inclui categorização da disparidade (Very High Gap, High Gap, Moderate Gap, Low Gap)

### 💊 Correlação com Drogas
- Há possibilidade de correlação entre cobertura de tratamento de drogas e taxas de suicídio
- Países com maior capacidade de tratamento podem apresentar taxas diferentes de suicídio

### ⚠️ Alertas Críticos
- Identificação de países com mudanças bruscas (>20% em um ano ou >50% em 5 anos) que necessitam atenção imediata
- Sistema de alertas categoriza mudanças como Sharp Increase/Decrease (1 ano) ou Major Increase/Decrease (5 anos)

---

## 🧪 Tecnologias

- **Databricks** (Repos, Notebooks, Unity Catalog, Lakeview)
- **Python** / **PySpark** para processamento distribuído
- **SQL** para modelagem e análise
- **WHO GHO API** para dados de saúde pública
- **OWID** para dados de HDI
- **AWS S3** para storage (landing zone)
- Arquitetura **Medalhão** (Bronze/Silver/Gold)

## 🔄 Como Reproduzir no Databricks

1. **Clone o repositório** no Databricks Repos
2. **Configure o S3 bucket** (ou ajuste os paths para seu storage)
3. **Execute os notebooks na ordem:**
   
   **Bronze** (Ingestão):
   ```
   scr/WHO - Índice de Suicídio/Bronze.ipynb
   scr/World Bank - IDH/Bronze.ipynb
   scr/WHO - Uso de Drogas/Bronzes.ipynb
   ```
   
   **Silver** (Transformação):
   ```
   scr/WHO - Índice de Suicídio/Silver.ipynb
   scr/World Bank - IDH/Silver.ipynb
   scr/WHO - Uso de Drogas/Silvers.ipynb
   ```
   
   **Gold** (Modelagem):
   ```
   scr/WHO - Uso de Drogas/Golds.ipynb
   ```
   
   **Validação**:
   ```
   scr/Validações/Validações.ipynb
   ```

4. **Importe o dashboard** no Lakeview usando `Suicide.lvdash.json`
5. **Execute análises** usando `scr/WHO - Uso de Drogas/Insights.ipynb`

---

## 📚 Fontes de Dados

### 1. Taxa de Suicídio (WHO)
- **API**: [WHO GHO OData API - SDG 3.4.2](https://ghoapi.azureedge.net/api/SDGSUICIDE)
- **Período**: 2000-2024
- **Cobertura**: ~180 países
- **Granularidade**: País/Ano/Sexo

### 2. IDH - Índice de Desenvolvimento Humano
- **Fonte**: [Our World in Data - HDI](https://ourworldindata.org/grapher/human-development-index.csv)
- **Origem**: UNDP (United Nations Development Programme)
- **Período**: 1990-2022

### 3. Indicadores de Drogas (WHO)
- **API**: WHO GHO - 20 indicadores incluindo:
  - Cobertura de tratamento (SUD_TREATMENTSERVICES_COVERAGE)
  - Índice de capacidade de serviços (SUD_SERVICECAPACITYINDEX)
  - População PWID estimada (PWID_PSE_NUM)
  - Programas de reabilitação (SCSUD_REHAB)
  - Mortalidade por overdose em prisões (PRISON_D3_DEATHS_DRUG_MRATE)
  - [E mais 15 indicadores...]

---

## 📝 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

## 🤝 Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

## ⚠️ Nota sobre Dados Sensíveis

Este projeto trabalha com dados públicos agregados sobre saúde mental. Os dados são utilizados exclusivamente para fins de análise estatística e pesquisa em saúde pública, respeitando todas as diretrizes de privacidade e ética em pesquisa.

---

**Desenvolvido com Databricks + PySpark** 🚀