# Projeto de Engenharia de Dados 
Um projeto de engenharia de dados com foco no Databricks envolve o design, construção e manutenção da infraestrutura essencial para coleta, armazenamento, processamento e análise de dados. Esse projeto requer habilidades em linguagens como R e SQL, além do uso do GitHub para documentar o projeto. A engenharia de dados desempenha um papel crucial ao capacitar organizações a extrair insights, tomar decisões baseadas em dados e desenvolver aplicativos orientados por dados.

# Índice
1. [Objetivo](#objetivo)
2. [Definição do Problema](#definição-do-problema)
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
     - [3.5 Criação de Tabelas de Camada Prata](#35-criação-de-tabelas-de-camada-prata)
     - [3.6 ETL - Extrair, Transformar e Carregar (Prata - Ouro)](#36-etl---extrair-transformar-e-carregar-prata---ouro)
     - [3.7 Criação de tabelas de camadas de ouro](#37-criação-de-tabelas-de-camadas-de-ouro)
     - [3.8 Catálogo de Dados](#38-catálogo-de-dados)
   - [4. Análise](#4-análise)
     - [4.1 Qualidade dos dados](#41-qualidade-dos-dados)
     - [4.2 Resolução de Problemas](#42-resolução-de-problemas)
   - [5. Autoavaliação](#5-autoavaliação)


## Definição do problema
A educação superior desempenha um papel vital na formação de indivíduos qualificados e na promoção do desenvolvimento econômico e social. A qualidade das instituições de ensino superior é frequentemente avaliada por rankings globais, como o QS World Rankings, que consideram diversos critérios, incluindo reputação acadêmica, empregabilidade de graduados, proporção professor-aluno, e internacionalização. No entanto, interpretar e utilizar esses rankings pode ser um desafio tanto para instituições quanto para estudantes e empregadores. Compreender como diferentes fatores influenciam a posição das instituições nesses rankings é crucial para identificar pontos fortes e áreas que precisam de melhorias.

## Objetivo
O objetivo deste projeto é analisar os dados da base QS-WORLD-RANKINGS-2025 para identificar os fatores que mais impactam a posição das instituições de ensino superior nos rankings. Através dessa análise, pretendemos responder às seguintes perguntas:

- Quais são as 10 melhores instituições no ranking geral do QS em 2025? 
- Qual é a proporção média de professores para alunos nas instituições listadas? 
- Quais são as instituições com a maior pontuação em reputação acadêmica e reputação do empregador?
- Como a localização geográfica influencia a posição no ranking?
- Como a presença em redes de pesquisa internacionais se correlaciona com a reputação acadêmica?

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

#### 2.1 Definição de Sistema de Computação em Nuvem
Para este projeto, o Databricks será a plataforma principal de processamento e análise de dados na nuvem. A escolha do Databricks como plataforma baseia-se em sua capacidade robusta de processamento distribuído e análise de dados em escala. Esta ferramenta é essencial para viabilizar o processamento eficiente e a extração de insights a partir dos dados utilizados no projeto de engenharia de dados.

#### 2.2 Recursos de armazenamento
Inicialmente, uma conta community foi criada no Databricks para fins acadêmicos. Aqui estão os recursos criados em ordem:

- Uma conta de armazenamento no Databricks, que fornece armazenamento em nuvem para arquivos, usando o Databricks File System (DBFS).
- Pastas de bronze, prata e ouro foram configuradas no Databricks para categorização e gerenciamento eficiente dos dados conforme sua importância e utilização no projeto de engenharia de dados.
  
Neste projeto, será implementada a arquitetura Medallion para o data lake utilizando o Databricks. Essa arquitetura oferece uma abordagem estruturada e eficiente para gerenciar e processar grandes volumes de dados. Ao empregar a arquitetura Medallion, o objetivo é otimizar os processos de ingestão, armazenamento e recuperação de dados, assegurando escalabilidade e confiabilidade. Com o data lake centrado na arquitetura Medallion, espera-se melhorar a acessibilidade aos dados, fortalecer as capacidades analíticas e aumentar a agilidade na geração de insights para suportar decisões informadas.

**Camadas do Data Lake:**
**Bronze:** Armazenamento de dados brutos no formato de coleção, como JSON, CSV, XLS, Parquet, organizados em pastas no Databricks.
**Prata:** Dados limpos e transformados, com remoção de colunas indesejadas, caracteres especiais e espaços, também organizados em pastas no Databricks.
**Ouro:** Dados organizados com aplicação de junções entre tabelas e regras de negócio conforme métricas e perguntas definidas para facilitar a análise e tomada de decisões, armazenados em pastas no Databricks.7

<div align="center">
  <img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/Fotos/ArquiteturaMedalhao.png"/>
</div>

### 3. Modelagem e Carregamento
A modelagem de dados é um processo essencial no campo da ciência da computação e gerenciamento de informações. Seu propósito fundamental é organizar, armazenar e gerenciar dados de maneira eficiente e precisa para atender às necessidades específicas de um projeto ou organização. Neste contexto, a Modelagem e o Carregamento de dados serão discutidos juntos, uma vez que o armazenando dos dados será feito em diferentes camadas no Databricks.

#### 3.1 Transformações no Databricks
Para realizar verificações nas transformações feitas nos dados brutos, será utilizado o Databricks como plataforma de análise de dados baseada em nuvem, que combina big data e recursos avançados de análise.
Após configurar o ambiente no Databricks, será criado um notebook para executar as verificações necessárias nas transformações dos dados brutos.

Agora iremos ler os dados de um arquivo CSV armazenado no DBFS (Databricks File System) e carregando-os em um DataFrame Spark usando sparklyr. 
A seguir, vou detalhar como essa parte se encaixa no fluxo geral de ingestão e transformação de dados.

```
%r
# Instalar e carregar o pacote necessário
install.packages("sparklyr")
library(sparklyr)

# Conectar ao Spark
sc <- spark_connect(method = "databricks")

# Caminho correto do arquivo no DBFS
file_path <- "dbfs:/FileStore/tables/qs_world_rankings_2025-10.csv"

# Renomear as colunas para remover caracteres inválidos
df <- df %>%
  dplyr::rename_all(~gsub(" ", "_", .)) %>%
  dplyr::rename_all(~gsub("[()]", "", .)) %>%
  dplyr::rename_all(~gsub("-", "_", .)) %>%
  dplyr::rename_all(~gsub("\\.", "", .)) %>%
  dplyr::rename_all(~gsub(",", "", .))

# Ler o arquivo CSV usando spark_read_csv
df <- spark_read_csv(sc, name = "qsworldrankings2025", path = file_path, header = TRUE, infer_schema = TRUE)

# Mostrar os primeiros registros do DataFrame após renomear colunas
print(head(df))
```

Feito isso, agora é possível criar tabelas e preenchê-las com dados do DBFS.

#### 3.2 Criação de Esquema
Dentro do Databricks, por viés organizacional, será necessário criar esquemas para armazenar as tabelas de análise. Será criado um esquema para cada camada do Data Lake. Para isso, basta abrir um notebook e utilizar os seguintes comandos SQL:

```
%sql
CREATE SCHEMA bronze;

CREATE SCHEMA silver;

CREATE SCHEMA gold;
```

#### 3.3 Criação de tabelas de camadas de bronze
No próprio Databricks, será aberto um notebook para verificar a qualidade dos dados presentes na camada Bronze. Para isso, será utilizado o uso do SPARK para ler os dados em CSV armazenados em conjunto com a criação de views:

**qs_world_rankings_2025**

**Tabela no esquema Bronze**

```
%sql
-- Criar a tabela no esquema bronze
CREATE TABLE bronze.qs_world_rankings_2025 USING CSV LOCATION 'dbfs:/FileStore/tables/qs_world_rankings_2025-10.csv'
OPTIONS ( 
  header = "true",  
  delimiter = ","
)
```

Nota: os tipos de dados ainda não foram definidos porque são dados brutos. Eles serão definidos na camada Silver.

#### 3.4 ETL - Extrair, Transformar e Carregar (Bronze - Prata)
Após inserir os dados brutos na camada Bronze, selecionar as colunas, perceber algumas inconsistências nos dados e criar as tabelas, o próximo passo é executar as transformações. Para essa tarefa, vamos aplicar transformações para preparar os dados para análise na camada Silver, tratando valores ausentes e ajustando os tipos de dados.

Abaixo estão as transformações usadas no Databricks:

```
%sql
-- Selecionar os dados da tabela na camada Bronze e aplicar transformações
CREATE OR REPLACE TEMP VIEW silver_data AS
SELECT
  `2025 Rank` AS `2025_Rank`,
  `Institution Name` AS `Institution_Name`,
  `Location`,
  CAST(`Academic Reputation` AS FLOAT) AS `Academic_Reputation`,
  CAST(`Employer Reputation` AS FLOAT) AS `Employer_Reputation`,
  CAST(`Faculty Student` AS FLOAT) AS `Faculty_Student`,
  CAST(REPLACE(`Citations per Faculty`, ',', '.') AS FLOAT) AS `Citations_per_Faculty`,
  CAST(`International Faculty` AS FLOAT) AS `International_Faculty`,
  CAST(`International Students` AS FLOAT) AS `International_Students`,
  CAST(`International Research Network` AS FLOAT) AS `International_Research_Network`,
  CAST(`QS Overall Score` AS FLOAT) AS `QS_OverallScore`
FROM bronze.qs_world_rankings_2025
WHERE `2025 Rank` IS NOT NULL 
  AND `Institution Name` IS NOT NULL 
  AND `Location` IS NOT NULL;
```

**Descrição das transformações:**
- Coleta de dados do Databricks
- `COALESCE` para substituir os valores nulos por 'Unknow' ou '0'.
- Conversão de Tipos de Dados: As colunas numéricas são convertidas para o tipo FLOAT, e a vírgula em Citations per Faculty é substituída por um ponto para permitir a conversão correta.
- Enviamos os dados transformados de volta ao Databricks, mas agora armazenados na camada Silver

#### 3.5 Criação de Tabelas de Camada Prata
O próximo passo é analisar os dados resultantes do processo ETL da camada Bronze para Silver. Para isso, será necessário criar uma nova tabelas após o ETL no Databricks>:

```
%sql
-- Escrever os dados transformados na camada Silver
CREATE TABLE silver.qs_world_rankings_transformed
USING PARQUET
AS
SELECT * FROM silver_data;
```

#### ETL - Extrair, Transformar e Carregar (Prata - Ouro)
Agora, será realizado o segundo e último ETL, que será relacionado da camada Silver para Gold. Aqui, foi a remoção dos dados null da coluna QS_OverallScore pois iria atrapalhar a nossa análise final e nossas perguntas que serão respondidas:

Descrição das transformações:
- Coleta de dados do Databricks
- Remover dados da coluna QS_OverallScore que são null
- Enviamos os dados transformados de volta ao Databricks, mas agora armazenados na camada Gold

**Criar a Visualização Temporária Filtrada**
```
%sql
-- Criar a visualização temporária com os dados filtrados da camada Silver
CREATE OR REPLACE TEMP VIEW gold_data AS
SELECT *
FROM silver.qs_world_rankings_transformed
WHERE QS_OverallScore IS NOT NULL;
```

#### 3.7 Criação de tabelas de camadas de ouro
Por fim, agora é possível realizar a análise final de forma muito mais prática, rápida e consistente, pois só temos colunas utilizáveis ​​de acordo com as regras de negócio das análises.

**Escrever os dados filtrados na camada Gold**

```
%sql
-- Criar a tabela na camada Gold
CREATE TABLE gold.qs_world_rankings_final
USING PARQUET
AS
SELECT * FROM gold_data;
```

#### 3.8 Catálogo de Dados
Um catálogo de dados é uma ferramenta que organiza e descreve informações sobre conjuntos de dados disponíveis, fornecendo detalhes como origem, estrutura, significado e relacionamento entre eles. É essencial para o gerenciamento e uso eficiente de dados em uma organização. Abaixo está o catálogo para a tabela final na camada Gold:

| ID | VARIAVEL | DESCRIÇÃO | TIPO | MINIMO | MAXIMO |
|----|----------|-------------|------|---------|---------|
| 1 | 2025_Rank | Posição da instituição nos rankings de 2025 | STRING | 1 | 1400 |
| 2 | Institution_Name | Nome da instituição de ensino superior | STRING | Massachusetts Institute of Technology (MIT) | Jilin University |
| 3 | Location | Localização geográfica da instituição | STRING | US | CN |
| 4 | Academic_Reputation | Pontuação que reflete a reputação acadêmica da instituição | FLOAT | 0 | 100 |
| 5 | Employer_Reputation | Pontuação que reflete a reputação do empregador | FLOAT | 0 | 100 |
| 6 | Faculty_Student | Relação entre o número de alunos e o corpo docente | FLOAT | 0 | 100 |
| 7 | Citations_per_Faculty | Pontuação que reflete as citações recebidas por cada membro do corpo docente | FLOAT | 0 | 100 |
| 8 | International_Faculty | Percentual de corpo docente origem internacional | FLOAT | 0 | 100 |
| 9 | International_Students | Percentual de alunos de origem internacional| FLOAT | 0 | 100 |
| 10 | International_Research_Network | Resultados de emprego dos graduados da instituição | FLOAT | 0 | 100 |
| 11 | QS_OverallScore | Pontuação geral da instituição no QS World University Rankings | FLOAT | 0 | 100 |

### 4. Análise
A análise de dados desempenha um papel crucial em um mundo cada vez mais digital e centrado em informações, abrangendo áreas que vão desde o mundo empresarial até a pesquisa acadêmica. Empresas de tecnologia líderes buscam se orientar cada vez mais por dados. Nesta fase final, a análise se concentrará nos indicadores essenciais utilizados para avaliar a excelência acadêmica, a diversidade internacional, o impacto da pesquisa e a empregabilidade de universidades em todo o mundo.

#### 4.1 Qualidade dos dados
Antes de nos aprofundarmos na análise propriamente dita, é crucial realizar uma avaliação da qualidade dos dados contidos na camada ouro (camada final) para entender de forma abrangente como esses dados podem influenciar as análises finais a serem conduzidas. Nesse contexto, nossa atenção será dedicada à identificação de possíveis inconsistências ou falhas nos dados, visando garantir que as análises subsequentes sejam baseadas em informações confiáveis.

Com base na nossa ultima camada gold toda alteração e tratamento foi realizado logo para os dados restantes, nenhum problema foi encontrado e iremos aproveitar toda a camada gold. 

#### 4.2 Resolução de Problemas
Nesta seção, serão apresentadas análises e respostas às questões levantadas sobre a educação em instituições de ensino superior. Por meio de representações gráficas e análises, serão fornecidos insights sobre diferentes aspectos da educação em instituições de ensino superior. Ao longo desta seção, serão utilizados gráficos e análises que abordam questões-chave, incluindo localização das instituições, proporção de alunos por corpo docente, reputação acadêmica e do empregador, além de fatores que impactam a pontuação geral do QS. Para todas as análises abaixo, SQL foi usada a (Structured Query Language).

**1. Quais são as 10 melhores instituições no ranking geral do QS em 2025?**

<details>
  <summary>Show Answer</summary>
  
<img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/graficos/1-10MelhoresInstituicoes.png" align="left"
     alt="melhores_instituicoes">   


Query:
```
%sql
-- Selecionar as top 10 instituições no ranking do QS em 2025
SELECT Institution_Name, QS_OverallScore
FROM gold.qs_world_rankings_final
ORDER BY QS_OverallScore DESC
LIMIT 10;
```

**Resposta:** As principais instituições no ranking geral do QS em 2025 representam um conjunto diversificado de universidades globalmente reconhecidas pela excelência acadêmica. Aqui estão as 10 melhores instituições:
- Massachusetts Institute of Technology (MIT): 100
- Imperial College London: 98.5
- University of Oxford: 96.9
- Harvard University: 96.8
- University of Cambridge: 96.7
- Stanford University: 96.1
- ETH Zurich - Swiss Federal Institute of Technology: 93.9
- National University of Singapore (NUS): 93.7
- UCL: 91.6
- California Institute of Technology (Caltech): 90.9

Essas universidades são líderes em suas respectivas áreas, refletindo um compromisso contínuo com a qualidade educacional e a pesquisa de ponta em escala global.

</details>
</details>

**2. Qual é a proporção média de professores para alunos nas instituições listadas?**

<details>
  <summary>Show Answer</summary>
  
<img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/graficos/2-M%C3%A9diaAlunosporProfessores.png)" align="left"
     alt="media_de_alunos_professores">

Query:
```
%sql
-- Calcular a proporção média de professores para alunos nas instituições listadas
SELECT AVG(Faculty_Student) AS Avg_Faculty_Student_Ratio
FROM  gold.qs_world_rankings_final;
```

**Resposta:** Isso significa que, em média, há aproximadamente 39 alunos por professor nas instituições listadas no seu conjunto de dados. Essa proporção é útil para entender a relação entre o corpo docente e o número de alunos, fornecendo uma medida geral da capacidade de atendimento e da relação aluno-professor nessas instituições.

</details>
</details>

**3. Quais são as instituições com a maior pontuação em reputação acadêmica e reputação do empregador?**

<details>
  <summary>Show Answer</summary>

  <img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/graficos/3-ReputacaoAlunoAcademia.png" align="left"
     alt="reputacao_aluno_academia">

Query:
```
%sql
-- Top 10 instituições com maior pontuação em reputação acadêmica e reputação do empregador combinadas
WITH Top_Academic AS (
    SELECT Institution_Name, Academic_Reputation
    FROM gold.qs_world_rankings_final
    ORDER BY Academic_Reputation DESC
    LIMIT 10
),
Top_Employer AS (
    SELECT Institution_Name, Employer_Reputation
    FROM gold.qs_world_rankings_final
    ORDER BY Employer_Reputation DESC
    LIMIT 10
)
SELECT 
    t1.Institution_Name,
    t1.Academic_Reputation AS Academic_Reputation_Score,
    t2.Employer_Reputation AS Employer_Reputation_Score
FROM Top_Academic t1
JOIN Top_Employer t2 ON t1.Institution_Name = t2.Institution_Name
ORDER BY (t1.Academic_Reputation + t2.Employer_Reputation) DESC;
```

**Resposta**: As instituições listadas apresentam pontuações perfeitas tanto em reputação acadêmica quanto em reputação do empregador, refletindo reconhecimento excepcional globalmente por sua excelência acadêmica e alta empregabilidade.

</details>
</details>

**4. Como a localização geográfica influencia a posição no ranking?**

<details>
  <summary>Show Answer</summary>

  <img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/graficos/4-MediaQSporLocalidade.png" align="left"
     alt="qs-por_localizacao">

Query:
``` 
%sql
-- Exemplo de consulta SQL para obter média do QS_OverallScore por localização geográfica
SELECT Location, AVG(QS_OverallScore) AS Avg_QS_OverallScore
FROM gold.qs_world_rankings_final
GROUP BY Location
ORDER BY Avg_QS_OverallScore DESC;
```

**Resposta:** A análise das médias do QS_OverallScore por localização geográfica revela padrões interessantes sobre como a posição no ranking é influenciada pela localização das instituições. Países como Hong Kong (HK) e Singapura (SG) emergem como líderes, com médias significativamente mais altas, indicando uma forte presença e desempenho acadêmico nessas regiões. Por outro lado, países como Islândia (IS), Bangladesh (BD) e Hungria (HU) mostram médias mais baixas, refletindo desafios potenciais ou menor representação no ranking global. Esses dados destacam a importância da localização geográfica na reputação e desempenho das instituições de ensino superior no cenário internacional.

</details>
</details>

**5. Como a presença em redes de pesquisa internacionais se correlaciona com a reputação acadêmica?**

<details>
  <summary>Show Answer</summary>

  <img src="https://github.com/Clarana12/-Clarana12-puc-ciencia-de-dados-e-analytics-mvp-sprint3/blob/main/graficos/5-RelacaoQSPesquisaInternacional.png" align="left"
     alt="qs_pesquisa_internacional">

Query:
```
%sql
-- Calcular a correlação entre International_Research_Network e QS_OverallScore
SELECT CORR(International_Research_Network, QS_OverallScore) AS Correlation
FROM gold.qs_world_rankings_final;
```

**Resposta:** Uma correlação de 0.477 indica uma relação moderada positiva entre a presença em redes de pesquisa internacionais (International Research Network) e a reputação acadêmica (QS_OverallScore). Aqui estão algumas interpretações com base nesse resultado:

**Relação Positiva Moderada:** A presença em redes de pesquisa internacionais tende a estar associada a uma reputação acadêmica mais elevada. Instituições que participam ativamente de colaborações internacionais de pesquisa podem ter maior visibilidade global e reconhecimento pela qualidade de sua pesquisa e ensino.

**Impacto na Posição no Ranking:** A participação em redes internacionais pode influenciar positivamente a posição de uma instituição no ranking QS. Isso sugere que instituições com uma forte presença internacional podem se beneficiar de uma reputação acadêmica mais alta, o que pode ser um diferencial competitivo significativo no cenário global da educação superior.

**Considerações para Estratégias Institucionais:** Para melhorar sua posição no ranking QS, instituições podem considerar investimentos em parcerias e colaborações internacionais, fortalecendo assim suas redes de pesquisa internacionais. Isso não apenas pode elevar a reputação acadêmica, mas também promover a excelência em pesquisa e ensino globalmente reconhecida.

Essas observações destacam a importância estratégica da colaboração internacional para as instituições que buscam melhorar seu perfil acadêmico e sua visibilidade global no ranking QS.

</details>
</details>


### 5. Autoavaliação
Durante o desenvolvimento deste projeto, optei por uma abordagem meticulosa e detalhada onde escrevi tudo que seria necessário fazer e no decorrer de toda a etapa fui finalizando meu checklist, o objetivo principal era tornar o processo de documentação no nível de excelência. Cada aspecto, desde a preparação inicial até a implementação no ambiente de computação em nuvem utilizando o Databricks, foi minuciosamente documentado e explicado. Essa abordagem não apenas me permitiu compreender profundamente cada etapa do processo que confesso não dominar quando o iniciei, mas também facilitou a revisão e a replicação do trabalho no futuro, onde posso usar como um guia. 

Integrei habilmente os conceitos teóricos aprendidos em sala de aula e as discursão que sempre temos com a turma. Isso incluiu a aplicação de técnicas avançadas de engenharia de dados no Databricks, como a criação de estruturas de dados eficientes, processos de ETL e análises detalhadas dos dados. A colaboração estreita com colegas e a orientação da universidade foram fundamentais para superar desafios técnicos complexos e explorar novas ferramentas, como o Databricks.

Embora enfrentar o ambiente de data lake e as peculiaridades da nuvem tenha sido desafiador, essa experiência foi transformadora. Além de aprimorar minhas habilidades técnicas, ela fortaleceu minha capacidade de resolver problemas de forma criativa e eficiente. Acredito sinceramente que esses desafios são oportunidades de crescimento e aprendizado, preparando-me para enfrentar futuros projetos com expertise e determinação.

Ao refletir sobre este projeto, reconheço o valor inestimável de uma abordagem disciplinada e colaborativa para alcançar resultados de alto impacto. Estou confiante de que as lições aprendidas e as habilidades desenvolvidas serão fundamentais para minha jornada profissional, capacitando-me para enfrentar os desafios e oportunidades que surgirem no futuro com conhecimento e confiança renovados.
