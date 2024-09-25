# Pipeline de analise de vendas de video games

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

Dataset: https://www.kaggle.com/datasets/gregorut/videogamesales

Este dataset contém uma lista de videogames com vendas superiores a 100.000 cópias. Foi gerado por meio de um scrape do site vgchartz.com.

[[Link para o Colab]](https://colab.research.google.com/drive/1RS7Sv9lGHmktiwjneEsMBmEhqS4LlNY8#scrollTo=9R8dTqvc356S)

