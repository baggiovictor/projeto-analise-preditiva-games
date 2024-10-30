# Análise Preditiva de Vendas de Videogames
**Autores:**
- Victor Hugo Baggio Alves
- Vinicius Ochner

## Sumário
1. [Visão Geral](#visão-geral)
2. [Domínio do Problema](#domínio-do-problema)
3. [Arquitetura de Dados](#arquitetura-de-dados)
4. [Metadados do Projeto](#metadados-do-projeto)
5. [Fonte de Dados](#fonte-de-dados)
6. [Conexão com Banco](#operações-principais)
7. [Metodologia](#metodologia)
8. [Análise Exploratória](#análise-exploratória)
9. [Recursos e Links](#recursos-e-links)

## Visão Geral
Este projeto visa realizar uma análise preditiva do mercado de videogames, utilizando um conjunto de dados abrangente sobre vendas de jogos que ultrapassaram 100.000 cópias. A análise combina técnicas de ciência de dados com um banco de dados NoSQL para fornecer insights valiosos sobre tendências e padrões do mercado.

## Domínio do Problema
O setor de videogames representa um mercado global em constante expansão, caracterizado por:

- **Volume de Dados:** Geração massiva de dados de vendas e métricas de engajamento
- **Variedade de Informações:** Combinação de dados categóricos (gênero, plataforma) e numéricos (vendas)
- **Valor Estratégico:** Insights críticos para publishers, desenvolvedores e investidores

## Arquitetura de Dados

### Justificativa do MongoDB Atlas
A escolha do MongoDB Atlas como solução de banco de dados se baseia em:

1. **Flexibilidade:** Esquema dinâmico para acomodar dados variáveis
2. **Escalabilidade:** Capacidade de crescimento automático conforme necessário
3. **Performance:** Otimização para operações de leitura em análises
4. **Gerenciamento:** Serviço totalmente gerenciado na nuvem
5. **Integração:** Facilidade de conexão com ferramentas de análise

### Modelo de Dados
Exemplo de documento no MongoDB:

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

## Metadados do Projeto

### Estrutura dos Metadados
```json
{
    "name": "analise-vendas-videogames",
    "owner_org": "catolica",
    "title": "Análise de Vendas de Videogames",
    "maintainer": "Victor Hugo Baggio Alves, Vinicius Ochner",
    "maintainer_email": "victor.alves@catolicasc.edu.br",
    "notes": "# Análise de Vendas de Videogames\r\n\r\nDataset contendo informações sobre jogos que venderam mais de 100.000 cópias, incluindo dados como:\r\n- Nome do jogo\r\n- Plataforma\r\n- Ano de lançamento\r\n- Gênero\r\n- Editora\r\n- Vendas em diferentes regiões geográficas",
    "state": "active",
    "resources": [{
        "name": "games.csv",
        "description": "Dataset completo de vendas de videogames com mais de 100.000 cópias vendidas",
        "format": "CSV",
        "url": "",
        "upload": "data/games.csv"
    }],
    "groups": [
        {"name": "esportes"},
        {"name": "rpg"}
    ],
    "tags": [
        {"name": "videogames"},
        {"name": "vendas"},
        {"name": "jogos"},
        {"name": "entretenimento"},
        {"name": "análise-preditiva"}
    ],
    "extras": [
        {
            "key": "Fonte dos Dados",
            "value": "Dataset obtido via kaggle"
        },
        {
            "key": "Período",
            "value": "Contém dados históricos de vendas de videogames"
        },
        {
            "key": "Metodologia",
            "value": "Dados coletados através de técnicas de etl, incluindo apenas jogos com vendas superiores a 100.000 cópias"
        }
    ]
}
```

### Descrição dos Campos de Metadados

1. **Identificação Básica**
   - `name`: Identificador único do dataset
   - `owner_org`: Organização proprietária
   - `title`: Título descritivo do dataset
   - `state`: Estado atual do dataset (ativo)

2. **Responsabilidade e Contato**
   - `maintainer`: Responsáveis pelo dataset
   - `maintainer_email`: Email para contato

3. **Recursos (Resources)**
   - Nome do arquivo: games.csv
   - Formato: CSV
   - Descrição detalhada do conteúdo:
        - Contém dados de vendas por país, ano, categoria e distribuidora
   - Método de upload local

4. **Categorização**
   - `groups`: Categorias principais (esportes, rpg)
   - `tags`: Palavras-chave para indexação
   

### Operações Principais

1. **Conexão ao Cluster:**
```python
uri = "mongodb+srv://user:senha@cluster2.4aum8c5.mongodb.net/?retryWrites=true&w=majority&appName=Cluster2"
client = MongoClient(uri)
db = client['videogames']
collection = db['videogames']
```

2. **Operações CRUD Básicas:**
- Inserção: `collection.insert_many(data_list)`
- Consulta: `collection.find()`
- Atualização: `collection.update_one()`
- Remoção: `collection.delete_one()`

## Metodologia

### Pré-processamento dos Dados

1. **Limpeza de Dados:**
```python
# Verificação de valores nulos
print("Valores nulos por coluna:")
print(df.isnull().sum())

# Remoção de registros incompletos
df_clean = df.dropna()
```

2. **Transformação de Variáveis:**
```python
# Codificação de variáveis categóricas
for col in ['genero', 'distribuidora', 'plataforma']:
    df_clean[f'{col}_cat'] = df_clean[col].astype('category').cat.codes
```

### Análise Exploratória

A análise exploratória inclui:
1. Matriz de correlação entre variáveis de vendas
2. Análise dos top 10 gêneros por vendas globais
3. Distribuição temporal de lançamentos
4. Estatísticas descritivas por região

## Recursos e Links

- **Dataset:** [Video Game Sales - Kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales)
- **Notebook:** [Google Colab](https://colab.research.google.com/drive/1RS7Sv9lGHmktiwjneEsMBmEhqS4LlNY8#scrollTo=9R8dTqvc356S)
- **MongoDB Atlas:** [Cluster](https://cloud.mongodb.com/v2/61928250173241641d5e8af9#/clusters)

### Notas Técnicas
- Critério de inclusão: Jogos com vendas > 100.000 cópias
- Período de análise: Histórico completo disponível no dataset
