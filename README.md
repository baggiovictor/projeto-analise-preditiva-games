# Projeto de análise preditiva

Aluno: Victor Hugo Baggio Alves

## a) Domínio do Problema

O domínio do problema apresentado refere-se à análise de dados de vendas de videogames. O dataset utilizado contém informações sobre jogos que venderam mais de 100.000 cópias, incluindo dados como nome do jogo, plataforma, ano de lançamento, gênero, editora e vendas em diferentes regiões geográficas.

Este domínio é particularmente interessante para Análise de Dados (AP) devido a:

1. Volume de dados: O setor de videogames gera uma quantidade massiva de dados de vendas.
2. Variedade: Os dados incluem informações categóricas (como gênero e plataforma) e numéricas (vendas).
3. Valor: Análises desses dados podem fornecer insights valiosos para publishers, desenvolvedores e investidores.

## b) Justificativa da Escolha do Modelo NoSQL

A escolha do MongoDB Atlas para este problema se justifica por sua flexibilidade em lidar com esquemas variáveis, ideal para dados de jogos, escalabilidade automática para acomodar grandes volumes de vendas, performance otimizada para leitura essencial em análises, suporte a dados semi-estruturados que podem evoluir com o tempo e, por ser um serviço gerenciado na nuvem, elimina a necessidade de gerenciar infraestrutura, permitindo total foco na análise de dados.

## c) Modelo de Exemplo

No MongoDB Atlas, os dados são armazenados em formato de documento. Um exemplo de documento para este dataset seria:

```json
{
  "_id": ObjectId("..."),
  "nome": "Super Mario Bros.",
  "plataforma": "NES",
  "ano": 1985,
  "genero": "Platform",
  "publisher": "Nintendo",
  "na_sales": 29.08,
  "europa_sales": 3.58,
  "japan_sales": 6.81,
  "other_sales": 0.77,
  "global_sales": 40.24
}
```

Este modelo permite armazenar todos os dados relevantes de cada jogo em um único documento.

## d) Exemplos de Manipulação de Dados

O código fornecido demonstra várias operações de manipulação de dados no MongoDB Atlas:

1. Conexão ao cluster:
```python
uri = "mongodb+srv://user:senha@cluster2.4aum8c5.mongodb.net/?retryWrites=true&w=majority&appName=Cluster2"
client = MongoClient(uri)
db = client['videogames']
collection = db['videogames']
```

2. Inserção de dados:
```python
collection.insert_many(data_list)
```

3. Consulta de dados:
```python
all_documents = collection.find()
for doc in all_documents:
    pprint(doc)
```

4. Atualização de dados:
```python
collection.update_one({}, {'$set': {'Publisher': 'Nintendo Updated'}})
```

5. Remoção de dados:
```python
collection.delete_one({})
```

Estas operações demonstram as inserções em massa, consultas flexíveis, atualizações pontuais e remoções de documentos.

## e) Justificativa para uso do MongoDB Atlas como Data Lake


A escolha do MongoDB Atlas como Data Lake para a indústria de videogames é ideal devido à sua flexibilidade para lidar com diversos tipos de dados, escalabilidade automática para acompanhar o crescimento do setor, modelo de dados adaptável à constante evolução dos jogos, capacidades analíticas integradas, facilidade de conexão com ferramentas de BI, segurança robusta para dados sensíveis e gerenciamento simplificado que libera a equipe para focar na análise estratégica em vez da manutenção da infraestrutura. Essa abordagem completa permite não só analisar as vendas atuais, mas também incorporar dados futuros de diversas fontes, criando um ambiente unificado e escalável para insights abrangentes sobre o mercado de jogos.

### https://cloud.mongodb.com/v2/61928250173241641d5e8af9#/clusters

---

# Pré-processamento dos Dados e Análise Descritiva

Após a importação e armazenamento inicial dos dados no MongoDB Atlas, foi realizado uma série de etapas de pré-processamento e análise descritiva para melhor compreender e preparar os dados para análises mais aprofundadas.

### 1. Limpeza de Dados

```python
print("Valores nulos por coluna:")
print(df.isnull().sum())
```

Em seguida, foi removido as linhas que continham valores nulos para garantir a integridade dos dados:

```python
df_clean = df.dropna()
print(f"Linhas removidas: {len(df) - len(df_clean)}")
```

### 2. Análise Descritiva dos Dados (ADD)

Foi feito  uma análise descritiva para entender melhor as características estatísticas dos nossos dados:

```python
print("Estatísticas descritivas:")
print(df_clean.describe())

print("\nTipos de dados:")
print(df_clean.dtypes)
```

Esta análise  forneceu informações sobre a distribuição dos dados, incluindo médias, medianas, valores mínimos e máximos para as variáveis numéricas, bem como os tipos de dados de cada coluna.

### 3. Transformação de Variáveis Categóricas

Para facilitar análises estatísticas futuras, foi ajustado as variáveis categóricas 'genero', 'distribuidora' e 'plataforma' em categorias numéricas:

```python
for col in ['genero', 'distribuidora', 'plataforma']:
    df_clean[f'{col}_cat'] = df_clean[col].astype('category').cat.codes
    print(f"\nMapeamento de {col}:")
    print(dict(enumerate(df_clean[col].astype('category').cat.categories)))
```

Este ajuste nos permite utilizar estas variáveis em modelos estatísticos que requerem entradas numéricas.

### 4. Análise Exploratória dos Dados (AED)

Por fim, foi realizado uma análise exploratória mais profunda, incluindo visualizações:

1. Matriz de Correlação: Criamos uma matriz de correlação entre as variáveis numéricas de vendas para identificar possíveis relações entre diferentes mercados.

2. Top 10 Gêneros: Analisamos os 10 gêneros de jogos com maiores vendas globais, fornecendo insights sobre as preferências do mercado.

3. Distribuição de Jogos por Ano: Visualizamos a distribuição do número de jogos lançados ao longo dos anos, permitindo identificar tendências temporais na indústria.

Estas visualizações nos permitem extrair insights valiosos sobre as tendências de vendas, popularidade de gêneros e evolução do mercado de jogos ao longo do tempo.

O pré-processamento e a análise descritiva realizados fornecem uma base sólida para análises mais aprofundadas e para o desenvolvimento de modelos preditivos relacionados à indústria de jogos. Eles permitem entender melhor a estrutura e as características dos dados, identificar possíveis problemas ou outliers, e começar a formular hipóteses sobre os fatores que influenciam o sucesso das vendas de videogames.


# Iformações

Dataset: https://www.kaggle.com/datasets/gregorut/videogamesales

Este dataset contém uma lista de videogames com vendas superiores a 100.000 cópias. Foi gerado por meio de um scrape do site vgchartz.com.

[[Link para o Colab]](https://colab.research.google.com/drive/1RS7Sv9lGHmktiwjneEsMBmEhqS4LlNY8#scrollTo=9R8dTqvc356S)
[[mongodb]](https://cloud.mongodb.com/v2/61928250173241641d5e8af9#/clusters)
