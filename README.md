# Projeto de Engenharia de Dados **Melhorar o texto**
Um projeto de engenharia de dados com foco no Databricks envolve o design, construção e manutenção da infraestrutura essencial para coleta, armazenamento, processamento e análise de dados. Esse projeto requer habilidades em linguagens como R e Python, além do uso do GitHub para controle de versão. A engenharia de dados desempenha um papel crucial ao capacitar organizações a extrair insights, tomar decisões baseadas em dados e desenvolver aplicativos orientados por dados.

# Índice
1. [Objetivo](#objetivo)
2. [Definição do Problema](#definicao-do-problema)
3. [O Projeto](#o-projeto)
   - [1. Pesquisa de Dados](#1-pesquisa-de-dados)
   - [2. Coleta de Dados](#2-coleta-de-dados)
     - [2.1 Definição de Sistema de Computação em Nuvem](#21-definizao-de-sistema-de-computacao-em-nuvem)
     - [2.2 Recursos de armazenamento](#22-recursos-de-armazenamento)
   - [3. Modelagem e Carregamento](#3-modelagem-e-carregamento)
     - [3.1 Conexão de Data Lake e Databricks](#31-conexao-de-data-lake-e-databricks)
     - [3.2 Criação de Esquema](#32-criacao-de-esquema)
     - [3.3 Criação de tabelas de camadas de bronze](#33-criacao-de-tabelas-de-camadas-de-bronze)
     - [3.4 ETL - Extrair, Transformar e Carregar (Bronze - Prata)](#34-etl-extrair-transformar-carregar-bronze-prata)
     - [3.5 Criação de Tabelas de Camada Prata](#35-criacao-de-tabelas-de-camada-prata)
     - [3.6 ETL - Extrair, Transformar e Carregar (Prata - Ouro)](#36-etl---extrair-trasformar-e-carregar-prata-ouro)
     - [3.7 Criação de tabelas de camadas de ouro](#37-criacao-de-tabelas-de-camadas-de-ouro)
     - [3.8 Catálogo de Dados](#38-catalogo-de-dados)
   - [4. Análise](#4-analise)
     - [4.1 Qualidade dos dados](#41-qualidade-de-dados)
     - [4.2 Resolução de Problemas](#42-resulucao-de-problema)
   - [5. Autoavaliação](#5-auto-avaliacao)


## Definição de problema
A educação superior desempenha um papel vital na formação de indivíduos qualificados e na promoção do desenvolvimento econômico e social. A qualidade das instituições de ensino superior é frequentemente avaliada por rankings globais, como o QS World Rankings, que consideram diversos critérios, incluindo reputação acadêmica, empregabilidade de graduados, proporção professor-aluno, e internacionalização. No entanto, interpretar e utilizar esses rankings pode ser um desafio tanto para instituições quanto para estudantes e empregadores. Compreender como diferentes fatores influenciam a posição das instituições nesses rankings é crucial para identificar pontos fortes e áreas que precisam de melhorias.


## Objetivo
O objetivo deste projeto é analisar os dados da base QS-WORLD-RANKINGS-2025 para identificar os fatores que mais impactam a posição das instituições de ensino superior nos rankings. Através dessa análise, pretendemos responder às seguintes perguntas:

- Quais fatores têm a maior correlação com a posição geral de uma instituição no ranking QS?
- Como a localização geográfica influencia a posição no ranking?
- Qual é a relação entre a reputação acadêmica e do empregador e a posição no ranking?
- De que forma a proporção professor-aluno e as citações por corpo docente afetam a posição da instituição?
- Como a presença de professores e alunos internacionais contribui para a classificação?
- Quais são os impactos dos resultados de emprego e do desempenho em sustentabilidade nas posições das instituições?

Através destas análises, buscamos fornecer insights valiosos para instituições de ensino superior, estudantes, e formuladores de políticas educacionais, ajudando a melhorar a qualidade e a competitividade das instituições de ensino superior em nível global.

## O projeto
### 1. Pesquisa de dados
A pesquisa de dados foi realizada utilizando informações disponíveis no site [Top Universities](https://www.topuniversities.com/world-university-rankings), que permite a seleção de diversos filtros para personalizar as classificações universitárias globais. No entanto, para a simplicidade e uniformidade da análise, optou-se por utilizar o conjunto de dados disponibilizado pelo Kaggle, que oferece uma compilação abrangente e padronizada das classificações para o ano de 2025.

Foram selecionadas as seguintes tabelas para análise:

QS World University Rankings 2025:[Top Universities](https://raw.githubusercontent.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/main/qs-world-rankings-2025.csv)

Esta tabela apresenta uma visão completa das classificações das universidades em 2025, incluindo várias métricas e indicadores essenciais para avaliar a excelência acadêmica, diversidade internacional, impacto da pesquisa e empregabilidade.

Nota: o site está em inglês (EN).

**Os conjuntos de dados foram armazenados no GitHub.**

### 2. Coleta de dados
A coleta de dados foi realizada baixando o arquivo CSV intitulado qs-classificações mundiais-2025.csv do Kaggle. Esta etapa foi crucial para garantir a precisão e a confiabilidade dos dados, uma vez que o Kaggle é amplamente reconhecido como uma plataforma de compartilhamento de dados confiável e de alta qualidade.

O conjunto de dados abrange diversas métricas importantes, tais como:

- Classificação da instituição
- Nome
- Localização
- Categoria de tamanho
- Pontuações de reputação acadêmica e do empregador
- Proporção professor-aluno
- Citações por corpo docente
- Proporções de professores e alunos internacionais
- Presença em redes de pesquisa internacionais
- Resultados de emprego
- Desempenho de sustentabilidade
- Pontuação geral do QS

Essas métricas oferecem insights valiosos sobre o panorama global das instituições de ensino superior, facilitando a análise comparativa e a tomada de decisões informadas por várias partes interessadas, incluindo estudantes, educadores, decisores políticos e empregadores.

#### Definição de Sistema de Computação em Nuvem
Para este projeto, o Databricks será a plataforma principal de processamento e análise de dados na nuvem. A escolha do Databricks como plataforma baseia-se em sua capacidade robusta de processamento distribuído e análise de dados em escala. Esta ferramenta é essencial para viabilizar o processamento eficiente e a extração de insights a partir dos dados utilizados no projeto de engenharia de dados.

#### 2.2 Recursos de armazenamento
Inicialmente, uma conta community foi criada no Databricks para fins acadêmicos. Aqui estão os recursos criados em ordem:

- Uma conta de armazenamento no Databricks, que fornece armazenamento em nuvem para arquivos, usando o Databricks File System (DBFS).
- Pastas de bronze, prata e ouro foram configuradas no Databricks para categorização e gerenciamento eficiente dos dados conforme sua importância e utilização no projeto de engenharia de dados.
  
Neste projeto, será implementada a arquitetura Medallion para o data lake utilizando o Databricks. Essa arquitetura oferece uma abordagem estruturada e eficiente para gerenciar e processar grandes volumes de dados. Ao empregar a arquitetura Medallion, o objetivo é otimizar os processos de ingestão, armazenamento e recuperação de dados, assegurando escalabilidade e confiabilidade. Com o data lake centrado na arquitetura Medallion, espera-se melhorar a acessibilidade aos dados, fortalecer as capacidades analíticas e aumentar a agilidade na geração de insights para suportar decisões informadas.

**Camadas do Data Lake:**
**Bronze:** Armazenamento de dados brutos no formato de coleção, como JSON, CSV, XLS, Parquet, organizados em pastas no Databricks.
**Prata:** Dados limpos e transformados, com remoção de colunas indesejadas, caracteres especiais e espaços, também organizados em pastas no Databricks.
**Ouro:** Dados organizados com aplicação de junções entre tabelas e regras de negócio conforme métricas e perguntas definidas para facilitar a análise e tomada de decisões, armazenados em pastas no Databricks.

### 3. Modelagem e Carregamento
A modelagem de dados é um processo essencial no campo da ciência da computação e gerenciamento de informações. Seu propósito fundamental é organizar, armazenar e gerenciar dados de maneira eficiente e precisa para atender às necessidades específicas de um projeto ou organização. Neste contexto, a Modelagem e o Carregamento de dados serão discutidos juntos, uma vez que um sistema Data Lake será diretamente utilizado, armazenando os dados em diferentes camadas no Databricks.

#### 3.1 Conexão de Data Lake e Databricks
Para realizar verificações nas transformações feitas nos dados brutos, será utilizado o Databricks como plataforma de análise de dados baseada em nuvem, que combina big data e recursos avançados de análise.
Após configurar o ambiente no Databricks, será criado um notebook para executar as verificações necessárias nas transformações dos dados brutos.rvice

**Com os recursos criados, basta ir no Databricks, criar um notebook e utilizar o seguinte código Spark:**

```py
service_credential = dbutils.secrets.get(scope="<scope>",key="<service-credential-key>")

spark.conf.set("fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net", "OAuth")
spark.conf.set("fs.azure.account.oauth.provider.type.<storage-account>.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account>.dfs.core.windows.net", "<application-id>")
spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account>.dfs.core.windows.net", service_credential)
spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account>.dfs.core.windows.net", "https://login.microsoftonline.com/<directory-id>/oauth2/token")
```

Onde:

escopo = escopo secreto, criado no próprio Databricks
service-credential-key = chave de credencial do Key Vault
storage-account = Conta de armazenamento
application-id = ID do aplicativo de registro do aplicativo
directory-id = ID do diretório de registro do aplicativo
Feito isso, há uma conexão entre o Databricks e o Data Lake. Agora é possível criar tabelas e preenchê-las com dados do Lake.

#### 3.2 Criação de Esquema
Dentro do Databricks, por viés organizacional, será necessário criar esquemas para armazenar as tabelas de análise. Será criado um esquema para cada camada do Data Lake. Para isso, basta abrir um notebook e utilizar os seguintes comandos SQL:

```py
CREATE SCHEMA bronze;

CREATE SCHEMA silver;

CREATE SCHEMA gold;
```

#### 3.3 Criação de tabelas de camadas de bronze
No próprio Databricks, será aberto um notebook para verificar a qualidade dos dados presentes na camada Bronze. Para isso, será utilizado o uso do SPARK para ler os dados em CSV armazenados como BLOBS em conjunto com a criação de views:

**Table microdata_basic_education_2022**

Table View
```py
spark.read.options(delimiter = ';', header = True).csv('abfss://bronze@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/microdados_ed_basica_2022.csv').display()
```
Table Visualization
```py
spark.read.options(delimiter = ';', header = True).csv('abfss://bronze@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/microdata_basic_education_2022.csv').createOrReplaceTempView('microdata_basic_education_2022')
```
**Table school_retention_rate_2022**

Table View
```py
spark.read.options(delimiter = ';', header = True).csv('abfss://bronze@microdata_basic_education_2022.dfs.core.windows.net/microdados_ed_basica_2022/school_retention_rate_2022.csv').display()
```
Table Visualiation
```py
spark.read.options(delimiter = ';', header = True).csv('abfss://bronze@microdata_basic_education_2022.dfs.core.windows.net/microdata_basic_education_2022/school_retention_rate_2022.csv').createOrReplaceTempView('microdata_basic_education_2022')
```

With this, some inconsistencies in the data were observed, such as special characters and unwanted columns.
The data was stored in the BRONZE schema. For this activity, SQL commands were used:

**Table microdata_basic_education_2022**
```py
CREATE TABLE bronze.microdata_basic_education_2022 USING CSV LOCATION 'abfss://bronze@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/microdata_basic_education_2022.csv'
OPTIONS (
  header = "true",
  delimiter = ";"
)
```
**Table school_retention_rate_2022**
```py
CREATE TABLE bronze.rend_escolar_2022
USING CSV LOCATION 'abfss://bronze@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/school_retention_rate_2022.csv'
OPTIONS (
  header = "true",
  delimiter = ";"
)
```

Nota: os tipos de dados ainda não foram definidos porque são dados brutos. Eles serão definidos na camada Silver.

#### ETL - Extrair, Transformar e Carregar (Bronze - Prata)
Após inserir os dados brutos na camada Bronze, selecionar as colunas, perceber algumas inconsistências nos dados e criar as tabelas, o próximo passo é executar as transformações. Para essa tarefa, foi utilizado o Data Factoryrecurso desenho, por ser uma ferramenta visual e fácil de usar, e as transformações necessárias não são avançadas. A linguagem usada por esse recurso é chamada de "Data Flow Expression Language". Essa linguagem permite que você defina transformações de dados usando uma sintaxe semelhante ao SQL e inclui funções e operadores para executar transformação, filtragem, projeção e muito mais. Abaixo estão as transformações usadas no Data Factory:

![ETL - Bronze para Silver](https://github.com/bbucalonserra/data_engineering/blob/main/pictures/ETL_bronze_to_silver.PNG)


Descrição das transformações:
- Coleta de dados do Data Lake
- `SELECT` para selecionar as colunas usadas na análise
- `DERIVED COLUMN` para remover caracteres especiais e estranhos das colunas
- `SINK`  para enviar os dados transformados de volta ao Data Lake, mas agora armazenados na camada/contêiner Silver

#### 3.5 Criação de Tabelas de Camada Prata
O próximo passo é analisar os dados resultantes do processo ETL da camada Bronze para Silver. Para isso, será necessário criar as novas tabelas após o ETL no Databricks já com a tipologia de dados definida e as variáveis ​​de null ou not null também :

**Table microdata_basic_education_2022**
```py
CREATE TABLE silver.education_basic_2022
  (YEAR_CENSUS INT NOT NULL,
  REGION_NAME STRING NOT NULL,
  STATE_NAME STRING NOT NULL,
  MESOREGION_NAME STRING NOT NULL,
  ENTITY_NAME STRING NOT NULL,
  ENTITY_CODE INTEGER NOT NULL,
  DEPENDENCY_TYPE INT,
  SCHOOL_CATEGORY_PRIVATE INT,
  LOCATION_TYPE INT,
  QTY_BASIC_STUDENTS INT,
  QTY_BASIC_STUDENTS_FEMALE INT,
  QTY_BASIC_STUDENTS_MALE INT,
  QTY_DVD_EQUIPMENT INT,
  QTY_TV_EQUIPMENT INT,
  QTY_DIGITAL_WHITEBOARD_EQUIPMENT INT,
  QTY_MULTIMEDIA_EQUIPMENT INT,
  QTY_VCR_EQUIPMENT INT,
  QTY_SATELLITE_DISH_EQUIPMENT INT,
  QTY_COPIER_EQUIPMENT INT,
  QTY_OVERHEAD_PROJECTOR_EQUIPMENT INT,
  QTY_PRINTER_EQUIPMENT INT,
  QTY_MULTIFUNCTION_PRINTER_EQUIPMENT INT,
  QTY_FAX_EQUIPMENT INT,
  QTY_PHOTO_EQUIPMENT INT,
  QTY_COMPUTER INT,
  QTY_ADMINISTRATIVE_COMPUTER INT,
  QTY_EXISTING_ROOMS INT,
  HAS_INTERNET INT,
  HAS_INDIGENOUS_EDUCATION INT,
  INDIGENOUS_LANGUAGE_TYPE INT,
  INDIGENOUS_LANGUAGE_CODE_1 INT,
  INDIGENOUS_LANGUAGE_CODE_2 INT,
  INDIGENOUS_LANGUAGE_CODE_3 INT,
  HAS_INDIGENOUS_EDUCATIONAL_MATERIAL INT)
USING CSV LOCATION 'abfss://silver@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/basic_education_2022_silver'
OPTIONS (
  header = "true",
  delimiter = ","
)
```

**Table school_retention_rate_2022**
```py
CREATE TABLE silver.TX_REND_ESCOLAS_2022 
(
  YEAR INT NOT NULL, 
  REGION STRING NOT NULL,
  STATE STRING NOT NULL,
  MUNICIPALITY_CODE INT NOT NULL,
  MUNICIPALITY_NAME STRING,
  SCHOOL_CODE INT NOT NULL,
  SCHOOL_NAME STRING,
  LOCATION STRING,
  ADMINISTRATIVE_DEPENDENCY STRING,
  BASIC_EDUCATION_APPROVAL_RATE FLOAT,
  BASIC_EDUCATION_REPROVATION_RATE FLOAT,
  BASIC_EDUCATION_ABANDONMENT_RATE FLOAT
)
USING CSV LOCATION 'abfss://silver@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/school_retention_rate_2022_silver'
OPTIONS (
  HEADER = "true",
  DELIMITER = ","
)
```

#### ETL - Extrair, Transformar e Carregar (Prata - Ouro)
Agora, será realizado o segundo e último ETL, que será relacionado da camada Silver para Gold. Aqui, foi feita a junção das duas tabelas através da coluna School Code (1:1), foi calculada a soma total de equipamentos por escola (pois para a análise, interessa apenas saber a quantidade total e não separar por tipo de equipamento), e foram removidas mais algumas colunas não utilizadas:

![ETL - Silver para Gold](https://github.com/bbucalonserra/data_engineering/blob/main/pictures/ETL_silver_to_gold.PNG)

Descrição das transformações:
- Coleta de dados do Data Lake
- `JOIN`  para mesclar as duas tabelas
- `SELECT`  para remover algumas colunas
- `DERIVED COLUMN` para remover quaisquer caracteres especiais restantes
- `SINK` para enviar os dados transformados de volta ao Data Lake, mas agora armazenados na camada/contêiner Gold

#### 3.7 Criação de tabelas de camadas de ouro
Por fim, agora é possível realizar a análise final de forma muito mais prática, rápida e consistente, pois só temos colunas utilizáveis ​​de acordo com as regras de negócio das análises.

``` py
CREATE TABLE gold.EDUCATION_RETENTION_SCHOOLS_JOINED
(
  YEAR_CENSUS INT NOT NULL,
  REGION STRING NOT NULL,
  STATE_NAME STRING NOT NULL,
  STATE STRING NOT NULL,
  MUNICIPALITY_NAME STRING,
  MUNICIPALITY_CODE INTEGER,
  DEPENDENCY INTEGER,
  ADMINISTRATIVE_DEPENDENCY STRING,
  LOCATION STRING,
  LOCATION_TYPE INTEGER,
  SCHOOL_CODE INTEGER NOT NULL,
  SCHOOL_NAME STRING,
  PRIVATE_SCHOOL_CATEGORY INTEGER,
  DISTINCT_LOCATION INTEGER,
  BASIC_EDUCATION_ENROLLMENTS INTEGER NOT NULL,
  BASIC_EDUCATION_ENROLLMENTS_FEMALE INTEGER NOT NULL,
  BASIC_EDUCATION_ENROLLMENTS_MALE INTEGER NOT NULL,
  TOTAL_EQUIPMENTS INTEGER,
  COMPUTERS INTEGER,
  ADMINISTRATIVE_COMPUTERS INTEGER,
  EXISTING_ROOMS INTEGER,
  INTERNET INTEGER,
  INDIGENOUS_EDUCATION INTEGER,
  INDIGENOUS_LANGUAGE INTEGER,
  INDIGENOUS_LANGUAGE_1 INTEGER,
  INDIGENOUS_LANGUAGE_2 INTEGER,
  INDIGENOUS_LANGUAGE_3 INTEGER,
  INDIGENOUS_MATERIAL INTEGER,
  BASIC_EDUCATION_APPROVAL_RATE FLOAT, 
  BASIC_EDUCATION_REPROVATION_RATE FLOAT,
  BASIC_EDUCATION_ABANDONMENT_RATE FLOAT,
  PRIMARY KEY ("SCHOOL_CODE")
)

USING CSV LOCATION 'abfss://gold@basiceducation.dfs.core.windows.net/microdata_basic_education_2022/education_retention_schools_joined'
OPTIONS (
  HEADER = "true",
  DELIMITER = ","
)
```

#### 3.8 Catálogo de Dados
Um catálogo de dados é uma ferramenta que organiza e descreve informações sobre conjuntos de dados disponíveis, fornecendo detalhes como origem, estrutura, significado e relacionamento entre eles. É essencial para o gerenciamento e uso eficiente de dados em uma organização. Abaixo está o catálogo para a tabela final na camada Gold:


| ID | VARIABLE | DESCRIPTION | TYPE | MINIMUM | MAXIMUM |
|----|----------|-------------|------|---------|---------|
| 1 | YEAR_CENSUS | Year of the data | INT | 2022 | 2022 |
| 2 | REGION | Region | STRING | Midwest | South |
| 3 | STATE_NAME | State name | STRING | Acre | Tocantins |
| 4 | STATE | Federative Unit | STRING | AC | TO |
| 5 | MUNICIPALITY_NAME | Municipality name | STRING | Abadia de Goiás | Zumbi dos Palmares |
| 6 | MUNICIPALITY_CODE | Municipality code | INTEGER | 1100015 | 5300108 |
| 7 | DEPENDENCY | "1 - Federal 2 - State 3 - Municipal 4 - Private" | INTEGER | 1 | 4 |
| 9 | LOCATION | Rural or Urban | STRING | Rural | Urban |
| 10 | LOCATION_TYPE | Rural or Urban | INTEGER | 0 | 1 |
| 11 | SCHOOL_CODE | School code | INTEGER | 11000058 | 53086007 |
| 12 | SCHOOL_NAME | School name | STRING | 0101001 ESCOLA MUNICIPAL VICENTE LICINIO CARDOSO | ZUMBI DOS PALMARES EEF |
| 13 | PRIVATE_SCHOOL_CATEGORY | "1 - Private 2 - Community 3 - Confessional 4 - Philanthropic - Not applicable for public schools" | INTEGER | 1 | 4 |
| 14 | DISTINCT_LOCATION | "0 - The school is not in a distinct location area 1 - Settlement area 2 - Indigenous land 3 - Area where a remnant quilombola community is located" | INTEGER | 0 | 3 |
| 15 | BASIC_EDUCATION_ENROLLMENTS | Number of enrollments in basic education | INTEGER | 1 | 999 |
| 16 | BASIC_EDUCATION_ENROLLMENTS_FEMALE | Number of female enrollments in basic education | INTEGER | 0 | 999 |
| 17 | BASIC_EDUCATION_ENROLLMENTS_MALE | Number of male enrollments in basic education | INTEGER | 0 | 999 |
| 18 | TOTAL_EQUIPMENTS | Total technological equipment | INTEGER | 0 | 99 |
| 19 | COMPUTERS | Total computers | INTEGER | null | null |
| 20 | ADMINISTRATIVE_COMPUTERS | Total administrative computers | INTEGER | null | null |
| 21 | EXISTING_ROOMS | Number of existing rooms | INTEGER | 0 | 1 |
| 22 | INTERNET | Has internet or not (1 or 0) | INTEGER | 0 | 1 |
| 23 | INDIGENOUS_EDUCATION | "0 - No 1 - Yes" | INTEGER | 1 | 3 |
| 24 | INDIGENOUS_LANGUAGE | "1 - Only in Indigenous Language 2 - Only in Portuguese Language 3 - In Indigenous and Portuguese Language - Not applicable for schools without Indigenous School Education" | INTEGER | 1 | 3 |
| 25 | INDIGENOUS_LANGUAGE_1 | Indigenous Education - Language in which teaching is conducted - Indigenous Language - Language Code 1 | INTEGER | 1 | 999 |
| 26 | INDIGENOUS_LANGUAGE_2 | Indigenous Education - Language in which teaching is conducted - Indigenous Language - Language Code 2 | INTEGER | 100 | 999 |
| 27 | INDIGENOUS_LANGUAGE_3 | Indigenous Education - Language in which teaching is conducted - Indigenous Language - Language Code 3 | INTEGER | 126 | 999 |
| 28 | INDIGENOUS_MATERIAL | Socio-cultural and/or pedagogical instruments and materials in use in the school for the development of teaching and learning activities - Indigenous | INTEGER | 0 | 1 |
| 29 | BASIC_EDUCATION_APPROVAL_RATE | Basic education approval rate | FLOAT | null | null |
| 30 | BASIC_EDUCATION_REPROVATION_RATE | Basic education reprovation rate | FLOAT | null | null |
| 31 | BASIC_EDUCATION_ABANDONMENT_RATE | Basic education abandonment rate | FLOAT | 0.0 | 9.0 |



### 4. Análise
A análise de dados é uma prática essencial em um mundo cada vez mais digital e orientado por informações. Ela desempenha um papel fundamental em diversas áreas, do mundo empresarial à pesquisa acadêmica. O principal objetivo das grandes empresas de tecnologia é se tornarem cada vez mais orientadas por dados, ou seja, elas são guiadas por dados. Nesta etapa final, a análise se concentrará na educação em terras indígenas no Brasil.

#### 4.1 Qualidade dos dados
Antes de nos aprofundarmos na análise propriamente dita, é crucial realizar uma avaliação da qualidade dos dados contidos na camada ouro (camada final) para entender de forma abrangente como esses dados podem influenciar as análises finais a serem conduzidas. Nesse contexto, nossa atenção será dedicada à identificação de possíveis inconsistências ou falhas nos dados, visando garantir que as análises subsequentes sejam baseadas em informações confiáveis.

Ainda há alguns problemas com a qualidade dos dados para certas colunas. A coluna MUNICIPALITY_NAME ainda está obtendo o valor "�" para letras com acentos ou para a letra "ç" ("ainda" porque esse problema foi abordado no ETL da camada Bronze para Prata). Como esses são apenas problemas de nomenclatura, não afetarão as respostas fornecidas abaixo. No entanto, no caso de criar um painel de visualização de dados, por exemplo, um gráfico de mapa com caracteres "�", o Power BI não conseguirá identificar a localização do município. A coluna BASIC_EDUCATION_APPROVAL_RATE tem valores nulos em todo o processo de ETL por algum motivo. Isso impede que análises relacionadas à aprovação de alunos em escolas indígenas, uma comparação entre aprovações com alunos em áreas indígenas e escolas regulares sejam realizadas. A coluna EXISTING_ROOMS também tem valores nulos, possivelmente devido a alguma etapa do processo de ETL. Isso impede análises sobre o número de alunos por sala de aula em escolas em áreas indígenas ou verificações se a infraestrutura das escolas em áreas indígenas atende às necessidades da população. As colunas COMPUTERS e ADMINISTRATIVE_COMPUTERS também são nulas, possivelmente devido a alguma etapa do processo ETL. Isso impede responder perguntas sobre computadores em escolas indígenas ("A presença de computadores em escolas indígenas tem alguma influência na taxa de evasão?") e pode enviesar os resultados sobre equipamentos tecnológicos. Para os dados restantes, nenhum problema foi encontrado. No entanto, seria interessante remover algumas colunas para melhorar o processamento de dados em consultas, uma vez que nem todas as colunas foram utilizadas.


#### 4.2 Resolução de Problemas
Nesta seção, serão apresentadas uma análise e respostas às questões levantadas sobre a educação indígena no Brasil. Por meio de representações gráficas e análises, serão fornecidos insights sobre a educação em terras indígenas. Ao longo desta seção, haverá gráficos e análises abordando questões-chave, incluindo a localização das escolas em terras indígenas, taxas de evasão, disponibilidade de equipamentos tecnológicos, acesso à internet e idioma de instrução. Para todas as análises abaixo, SQLfoi usada a (Structured Query Language).


**1. Where are located the indiginous schools in Brazil?**

<details>
  <summary>Show Answer</summary>
  
<img src="https://github.com/bbucalonserra/data_engineering/blob/main/graphics/loc_escolas_indigenas.PNG" align="left"
     alt="loc_escola_indigena">

Query:
``` py
SELECT
STATE_NAME,
COUNT(SCHOOL_CODE) AS COUNT_SCHOOLS
FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
WHERE DISTINCT_LOCATION = 2
GROUP BY STATE_NAME
ORDER BY COUNT_SCHOOLS DESC
```

Response: Schools in indigenous lands are located in various states of Brazil. Based on the count of schools per state, we can identify the states with the highest number of schools in indigenous lands:
- Amazonas: 2,190 schools
- Roraima: 674 schools
- Maranhão: 642 schools
- Pará: 618 schools
- Acre: 456 schools

Therefore, schools in indigenous lands are mainly concentrated in the states of the Northern region, with Amazonas and Roraima leading in terms of the number of schools. This distribution reflects the presence of indigenous communities in these regions and the need for education in the areas of their lands.

</details>
</details>


**2. What is the dropout rate in indigenous schools? Is this value higher or lower than regular schools?**

<details>
  <summary>Show Answer</summary>
  
<img src="https://github.com/bbucalonserra/data_engineering/blob/main/graphics/Taxa_de_Abandono.PNG" align="left"
     alt="taxa_de_abandono">

Query:
``` py
WITH INDIGENOUS_ED AS (
  SELECT
    AVG(BASIC_EDUCATION_ABANDONMENT_RATE) AS AVERAGE_INDIGENOUS_EDUCATION
  FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
  WHERE
    DISTINCT_LOCATION = 2
    AND BASIC_EDUCATION_ABANDONMENT_RATE <> 0
    AND BASIC_EDUCATION_ABANDONMENT_RATE IS NOT NULL 
),

GENERAL_ED AS (
  SELECT
    AVG(BASIC_EDUCATION_ABANDONMENT_RATE) AS AVERAGE_BASIC_EDUCATION_GENERAL
  FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
  WHERE
    BASIC_EDUCATION_ABANDONMENT_RATE <> 0
    AND BASIC_EDUCATION_ABANDONMENT_RATE IS NOT NULL  
)

SELECT
  ROUND(INDIGENOUS_ED.AVERAGE_INDIGENOUS_EDUCATION, 2) AS AVERAGE_INDIGENOUS_ED,
  ROUND(GENERAL_ED.AVERAGE_BASIC_EDUCATION_GENERAL, 2) AS AVERAGE_GENERAL_ED,
  ROUND((INDIGENOUS_ED.AVERAGE_INDIGENOUS_EDUCATION - GENERAL_ED.AVERAGE_BASIC_EDUCATION_GENERAL), 2) AS PERCENTUAL_DIFFERENCE,
  ROUND((INDIGENOUS_ED.AVERAGE_INDIGENOUS_EDUCATION - GENERAL_ED.AVERAGE_BASIC_EDUCATION_GENERAL) / GENERAL_ED.AVERAGE_BASIC_EDUCATION_GENERAL * 100, 2) AS DIFFERENCE_IN_PERCENTAGE
FROM INDIGENOUS_ED, GENERAL_ED
```


Response: The dropout rate in indigenous schools is 18.59%, while in regular schools it is 7.32%. Therefore, we can conclude that the dropout rate in indigenous schools is considerably higher than in regular schools, with a difference of 11.27% higher than regular schools. This suggests that indigenous schools may face additional or different challenges that contribute to a higher dropout rate compared to non-indigenous schools. It is important to investigate and address these challenges to improve access and the quality of education for indigenous communities.

</details>
</details>



**3. What is the average number of technological equipment per state in schools with indigenous education?**

<details>
  <summary>Show Answer</summary>

  <img src="https://github.com/bbucalonserra/data_engineering/blob/main/graphics/media_equip_escolas_por_estado.PNG" align="left"
     alt="media_equipamentos_estado">

Query:
``` py
SELECT
  STATE_NAME,
  ROUND(AVG(TOTAL_EQUIPMENTS),2) AS AVERAGE_EQUIPMENTS
FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
WHERE
  BASIC_EDUCATION_ABANDONMENT_RATE IS NOT NULL
  AND BASIC_EDUCATION_ABANDONMENT_RATE <> 0
  AND DISTINCT_LOCATION = 2
GROUP BY ALL
ORDER BY AVERAGE_EQUIPMENTS DESC
```

Answer: The above graph shows the average number of technological equipment available in schools with indigenous education in each state. Santa Catarina has the highest average, with 9 equipment, while Mato Grosso, Tocantins, Mato Grosso do Sul, Acre, Amapá, and Maranhão have very low averages, close to zero. These numbers indicate the disparity in the availability of technological equipment in indigenous schools in different states of Brazil.

</details>
</details>

**4. What is the percentage of schools in indigenous locations that have internet access by state?**

<details>
  <summary>Show Answer</summary>


  <img src="https://github.com/bbucalonserra/data_engineering/blob/main/graphics/porcentagem_escolas_indigenas_com_internet.PNG" align="left"
     alt="internet_por_estado">

Query:
``` py
SELECT
  STATE_NAME,
  ROUND((SUM(CASE WHEN INTERNET = 1 THEN 1 ELSE 0 END) / COUNT(*)) * 100, 2) AS PERCENTAGE_WITH_INTERNET
FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
WHERE 
  DISTINCT_LOCATION = 2
GROUP BY STATE_NAME
ORDER BY PERCENTAGE_WITH_INTERNET DESC
```

Answer: The above numbers represent the percentage of indigenous schools in each state that have internet access. While some states, such as Paraná and Goiás, have 100% of their indigenous schools with internet access, others, such as Piauí and Acre, have a very low or even zero percentage of schools with internet access. This reflects the variation in information technology infrastructure in different regions of the country and highlights the need to improve internet access in indigenous schools across Brazil.

</details>
</details>

**5. In which language are subjects taught in indigenous schools? Are we maintaining the roots of the tribes regarding the mother tongue?**

<details>
  <summary>Show Answer</summary>


  <img src="https://github.com/bbucalonserra/data_engineering/blob/main/graphics/linguas_indigenas.PNG" align="left"
     alt="lingua_indigena">

Query:
``` py
SELECT
  INDIGENOUS_LANGUAGE,
  ROUND(COUNT(SCHOOL_CODE) * 100.0 / SUM(COUNT(SCHOOL_CODE)) OVER (), 2) AS PERCENTAGE_OF_SCHOOLS
FROM gold.EDUCATION_RETENTION_SCHOOLS_JOINED
WHERE
  DISTINCT_LOCATION = 2
GROUP BY INDIGENOUS_LANGUAGE
ORDER BY INDIGENOUS_LANGUAGE
```

Answer: In indigenous schools, subjects are taught in different languages, and some schools adopt a bilingual approach. Here is the distribution based on the data:
  - Indigenous language only: 3.30% of indigenous schools exclusively adopt the indigenous language as the medium of instruction
  - Portuguese: 22.70% of indigenous schools teach subjects only in Portuguese
  - Indigenous language and Portuguese: The majority of indigenous schools, 71.97%, adopt a bilingual approach, teaching subjects in both the indigenous language and Portuguese
  - Not applicable without indigenous education: 2.02% of the data is not applicable, indicating that these schools do not offer indigenous education or did not provide information about the language of instruction

Therefore, most indigenous schools in Brazil adopt a bilingual approach, teaching subjects in both the indigenous language and Portuguese, which reflects the importance of preserving the roots of the tribes regarding the mother tongue while providing access to education in Portuguese.

</details>
</details>


### 5. Autoavaliação
O projeto foi conduzido com uma abordagem extremamente detalhada, resultando em uma documentação que considero excelente. Cada linha de código e passo do sistema de computação em nuvem foi explicado, incluindo não apenas o que foi feito. Essa transparência e clareza contribuíram significativamente para meu entendimento do processo.

Além disso, o desenvolvimento deste trabalho foi integrado com estudos, abrangendo explicações detalhadas dos tipos de engenharia de dados realizados para utilização do Azure, criação de tabelas, processos de ETL e análises. Essa correlação entre o projeto prático e a fundamentação teórica foi muito importante, proporcionando um entendimento mais profundo e contextualizado de todo o processo analítico.

O sistema de computação em nuvem apresentou o maior desafio. No entanto, colhi insights inestimáveis ​​e um bom ambiente de data lake, aprimorando minha destreza técnica e habilidades de resolução de problemas. Apesar da dificuldade, navegar na nuvem provou ser um grande passo em meus estudos, equipando-me com o conhecimento e a confiança para enfrentar empreendimentos futuros.

