# O que é MongoDB?
Basicamente, MongoDB é um tipo de banco de dados **não-relacional**, ou **NoSQL**. Isso significa que ele não tem estruturas complexas como tabelelas, diferente de bancos de dados relacionais ou SQL.

Ele é **orientado a documentos**: em vez de tabelas e linhas, ele armazena dados em **documentos que parecem JSON (ou JSON-like)**, como pro exemplo o **BSON (ou Binary JSON)**.

# Quando usar?
Usar bancos de dados NoSQL como MongoDB faz sentido usar quando:
- Dados vem com **estrutura flexível**;
- Tem uma **evolução constante do modelo**;
- **Alto volume** de leitura/escrita;
- Necessidade de **escalabilildade horizontal**;
- Cosos como **catálogos, logs, perfis de usuários, eventos, cache, etc.**

# NoSQL vs SQL: qual a diferença?
O SQL tem: 
- **esquema rígido**;
- **joins fortes**; e
- **modelagem relacional**.

Enquanto NoSQLs tem:
- **Esquema flexível**;
- **Dados aninhados**; e
- **Menos dependência de joins**.

O MongoDB não susbtitui o SQL em qualquer cenário. Ele é melhor só quando o modelo documental e a escalabilidade horizontal fazem mais sentidos que relações complexas.

# Estruturas de dados
O MongoDB organiza dados em três níveis principais:
- **Banco de dados**: que é o container lógico;
- **Coleção**: que é o tipo uma tabela do SQL; e
- **Documento**: que é tipo uma linha (mas em formato de objeto);

Exemplo de um documento no MongoDB:

``` json
{
	"_id": 1,
	"nome": "Igor",
	"idade": 28,
	"enderecos": [
		{ "cidade": "São Paulo", "uf": "SP" }
	]
}
```

# BSON (Bê-son)
**BSON** é um formato binário usado **internamente** pelo MongoDB.
Ele meio que parece com o JSON, mas suporta tipos extras, como:
- Date;
- ObjectID;
- Decimal128;
- Binários;

Documentos podem ter **campos diferentes** de outro documento da mesma coleção.
O `_id` é o identificador únido padrão do objeto (o ID, dããããã)
Dados aninhados e array são comuns nesses tipos de objetos.

# Tipos de operações no MongoDB
O MongoDB suporta operações CRUD como qualquer outro banco de dados:
- Create;
- Read;
- Update;
- Delete.

Porém, operações de update usam operadores como:
- `$set`
- `$inc`
- `$push`
- `$pull`

Isso ajuda a não sobrescrever o documento inteiro quando somente um campo vai ser alterado.

# Consultas comuns
As operações em MongoDB geralmente usam:
- **Filtros**;
- **Projeções**; e
- **Ordenações**.

#### Filtros:
**Filtros** servem para buscar documentos que atendem as condições da busca.
Essas condições podem ser:
- Igualdade;
- Maior que / menor que;
- `in` (Se existe)
- `and` / `or`

#### Projeções:
**Projeções** definem quais campos retornar na busca.
Por exemplo:
- Trazer somente o `nome` e `idade` dos documentos;
- Esconder outros campos desnecessários.

Iso melhora a clareza e a performance da busca.

#### Odenação:
Bem, é o que diz o nome: ordena os resultados por um ou mais campos, em crescente ou decrescente.

# Índices
**Índices** servem para **acelerar consultas**.

Sem o Índice, o MongoDB tende a fazer a varredura da coleção de documentos.
Já com o Índice, ele consegue achar os registros mais rapidamente.

#### Tipos de índice:
- **Índice simples**;
- **Índice composto**;
- **Índice único**;
- **Índice em array**;
- **Texto** e **geoespacial** como noções extras

#### Quando usar:
Índices devem serem usados quando há **campos usados com frequência em filtros**, **campos em ordenação** ou quando há **campos com busca recorrente**.

#### Cuidado importante:
Os Índices melhoram a leitura, mas pode acabar **onerando a escrita**, deixando inserts/updates **mais caros**.

*É uma troca entre **performance de leitura** e **custo de manutenção de escrita**. Tem que saber se vale a pena para o determinado caso de uso.*

# Replicação e Sharding
### Replicação:
A **Replicação** é quando há uma cópia de um mesmo dado repetido em múltiplos nós. Ela permite uma **alta disponibilidade** desses dados e uma **tolerância a falhas**, já que o dado está em vários lugares ao mesmo tempo.

Isso também pode permitir uma leitura distribuida dependendo da configuração.

Normalmente existe dois tipos de **Replicação**:
- **Primária**; e
- **Secundária**.

A **Primária** recebe somente escritas, enquanto a **Secundária** recebe cópias sincronizadas do mesmo dado.

Se a **Primária** falhar, a outra pode assumir no lugar dela.

### Sharding:
O **Sharding** é a divisão dos dados entre múltiplos servidores.

Ela é importante porque permite uma **escalagem horizontal** dos dados. Ela **distribui os volumes** de **dados** e de **carga**, o que é **útil para bases muito grandes**

### Basicamente:
- **Replicação** = **redundância** e **disponibilidade**;
- **Sharding** = **escala** e **distribuição de dados**.

# MongoDB com Java
Em Java, normalmente usamos o **MongoDB Java Driver**. Ele nos permite **criar uma conexão com a instância** de MongoDB, para acessar o banco e coleção, **executar operações** e **mapear os documentos para classes** Java quando necessário

O fluxo básico é:
1. Conectar ao cluster/servidor;
2. Selecionar database;
3. Selecionar collection;
4. Executar operações;
5. Converter resultado para objeto Java (se necessário).

### Pontos que podem cair:
- Uso do `MongoClient`;
- Acesso a `MongoDatabase` e `MongoCollection`;
- Consultas com filtros;
- Integração com Spring Data MongoDB.

### É bom saber:
- Diferença entre **driver nativo** e **Spring Data MongoDB**
- Como fazer buscas por filtro;
- Como atualizar parte de um documento;
- Noção de `ObjectID`

# Teste de perguntas básicas:
1. *O que é MongoDB e qual a principal diferença dele em relação a um banco relacional?*
R: MongoDB é um banco de dados NoSQL, então ele não é dividido em tabelas e linhas, mas sim em coleções e documentos, documentos esses que podem ou não conter outros documentos aninhados. Ele é "schema-less" (sem esquema fixo), armazena dados em BSON e não tem suporte nativo a Joins.

2. *Qual a diferença entre documento, coleção e banco de dados no MongoDB?* 
R: Documento é a unidade básica dos dados, tipo uma linha do SQL. Coleções são onde ficam localizados os documentos, tipo uma tabela do SQL (mas sem schema fixo). O Banco de dados se refere ao agrupamento de coleções, tipo o database do SQL.

3. *O que é BSON e por que ele existe?*
R: Ele é um Binary JSON, que é uma forma binária de JSON usada internamente pelo MongoDB que possue alguns tipos de dados a mais que o JSON (Como `ObjectID`, `Date`, `BinData` e `Decimal128`) e é usado para agilizar o processamento de JSON pelo MongoDB

4. *Explique as operações CRUD no MongoDB com exemplos simples.*  
R:
Create: Inserir um novo documento em uma collection;
`db.usuarios.insertOne({ nome: "Ana", idade: 25})`

Read: Buscar uma informação em documentos com uma característica específica; 
`db.usuarios.find({ idade: { $gt: 18 } })`

Update: Alterar alguma informação em um documento específico; 
`db.usuarios.updateOne({ nome: "Ana", { $set: { idade: 26 } } })`

Delete: Deletar um documento de uma collection. 
`db.usuarios.deleteOne({ nome: "Ana" })`

6. *Para que servem índices e qual o trade-off de usá-los em excesso?*
R: Servem para agilizar a busca e leitura de documentos no banco. Mas os índices podem acabar onerando a inserção e escrita de documentos. Além disso, cada índice consome espaço em disco e memória RAM. E o campo `_id` já é indexado por padrão.

7. *Qual a diferença entre replicação e sharding?*
R: Replicação quando o banco inteiro é copiado em múltiplos nós, enquanto Sharding é quando os dados são particionados em múltiplos servidores.

8. *Em Java, como você se conectaria ao MongoDB e faria uma consulta básica?*
R: Usando o `spring-boot-starter-data-mongodb` do Spring Data, configurando a URI no `application.properties` e criando uma classe anotada com `@Document` em um `MongoRepository` ou `MongoTemplate` pra executar consultas.

9. *Como você buscaria todos os usuários com idade maior que 30, ordenados por nome, retornando apenas nome e idade?*
R: Aplica o filtro `idade > 30`, projeta apenas os campos `idade` e `nome`, e ordena por `nome`.

``` js
db.usuarios.find(
	{ idade: { $get 30 } },
	{ nome: 1, idade: 1, _ud: 0 }
).sort({ nome: 1 })
```
ou
```java
Query query = new Query(Criteria.where("idade").gt(30));
query.fields().include("nome").include("idade").exclude("id");
query.with(Sort.by("nome"));

mongoTemplate.find(query, Usuario.class);
```


11. *Quando devo usar um SQL ou NoSQL em uma aplicação?*
R: SQL é mais adequado quando tem relacionamentos complexos entre entidades, necessidade de consistência transacional (ACID) e um schema fixo.
NoSQL é melhor quando os dados tem estrutura variável, quando a escala horizontal é prioritária ou quando os dados são naturalmente hierárquicos.
Temos que basear nossa escolha pelo padrão de acesso e natureza dos dados, não necessariamente pelo volume

## Respostas curtas que você deve saber dizer
- **MongoDB é um banco documental NoSQL**
- **Documento é a unidade principal de dados**
- **BSON é o formato binário interno**
- **CRUD é criar, ler, atualizar e deletar**
- **Índice acelera leitura, mas custa escrita**
- **Replicação aumenta disponibilidade**
- **Sharding aumenta escalabilidade horizontal**
- **No Java, você usa o driver ou Spring Data MongoDB**







.
.
.
.
.
.
.
.
.
.
.
.
.
.
