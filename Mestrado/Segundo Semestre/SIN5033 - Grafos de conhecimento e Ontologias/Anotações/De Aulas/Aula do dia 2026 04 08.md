# Parte 1: Grafos
```mermaid
mindmap
Root(Grafos)
	(Pirâmide)
		("Operacional -> Tático -> Est")
		ETL

	(Tipos de bancos de dados:)		
		DataLake
			[Dados não estruturados]
		Data Warehouse
			[Dados estruturados]

	(Rótulos vs Aresta)
		*Quando usar um e usar outro?*
		[*Rótulos* são **descritivos**
		*Arestas* são **relacionais**]

	(🔑 Padrões de grafos:
	*- Básicos*
	*- Complexos*
	*- Navegacionais*)
		
		Navigacionais
			[Tipo o "X-path" do XML]
			["Expressões de caminho"]
			[Pode ter caminhos inversos]

	(Grafos de conhecimento)
		[🤔 Frequentemente usado por não-especialistas]
		

			
```

(Grafos de conhecimento)
🤔 Frequentemente usado por não-especialistas

```mermaid
mindmap
	root(Precisamos de uma interface de consulta)
		(Navegação facetada)
			(Ex Busca por palavra chave, por nó)
		(usuário explora iterativamente) 
			(Interface amigável e refinamento progressivo)
		(Query by example)
		(Exs de GUIs)
			[Broccoli]
			[VisiNav]
			[SemFacet]
			[GraFa]
		(Query answering systems)
			(Usa linguagem natural para fazer pesquisas)
		(Nova iniciativa usar LLMs para criar queries)
			(Muito bom)
				(mas pode dar erro em um caso específico)
					(não lembro qual kkkk)
				(Daí tem que usar views)

```


# Parte 2: Tecnologia de Big Data
```mermaid
mindmap
root(Big Data)
	Manipulação e processamento de grande quantidade de dados
		Mineração de dados
	Dados massivos
	[Conjunto de ferramentas orientadas à Big Data]
		Hadoop
		MongoDB
		VoltDB
		Spark
		etc.
	Nem toda gestão/análise de dados tradicional é boa
		))Nova tendência: NoSQL((
			NoSQL: não usa SGBDs relacionais tradicionais
			Outras techs relac. à armaz.\process. de dados em cluster:
				(Hadoop *-um pouco defazado no momento-*, spark, etc.)
		
			
	
```

NoSQL não significa que é SQL, só que não é relacional.

Precisamos de profissionais que lidam com grande volume de dados.

Analisar dados sempre existiu, mas agora temos demandas para especialistas (como engenheiro de dados, analista de dados, engenheiro de ML, etc.)

**Hadoop** é baseado em *MapReduce*. Apesar ser muito bom para simplificar, nem tudo pode ser solucionado com essa abordagem. *Map Reduce: Mapeia e reduz, agregando resultados.*

## Cientista de dados x Engenheiro de dados
- **Cientista de dados**:
	- Trabalha com a **descoberta de conhecimento** usando a análise de dados.
	- Utilizam técnicas matemáticas e algoritmos para solucionar problemas de negócio.
- **Engenheiro de dados**:
	- Trabalha para processar e tratar dados pra serem usados em aplicações de Big Data.
	- Utilizam conhecimento de ciência da computação p/ criar sistemas e resolver problemas de processamento de dados em **tempo real** e manipular quantidades imensas de dados.

## **Cinco "Vês" do Big Data**
- Volume 
- Velocidade
- Variedade
- Veracidade
- Valor

## Caracterização de Big Data
Pode ser caracterizado por :
- **Grande volume de dados**: Terabytes, Petabytes, etc.
- **Tipos de dados variados**: Armazenamento de dados complexos.
- **Armazenamento em clusters**: Clusters de processadores de baixo custo, distribuídos de forma transparente.
- **Poder de crescimento elástico horizontal**: Alocação/desalocação de recursos sob demanda.

# Cloud Computing
Tem recentemente sido utilizados para o gerenciamento de dados em Big Data.
DaaS -> Data as a Service
IaaS -> Infrastructure as a Service

Cloud permite escalabilidade, elasticidade, funcionamento em *commodity* hardware.

Cloud pode ser:
- Single Tenant; ou
- Multitenant.

# Big Data: Por que o interesse agora?
Fontes de dados diversificados, de vários lugares, em grande peso. 
Os dados são valiosos demais para serem deletados.
Nos últimos tempos, houve uma redução drástica no custo do hardware, principalmente no de armazenamento.
Também houve um crescimento de soluções de Cloud.

Gerenciamento de dados foi **Democratizado**.

# Tecnologias NoSQL:
"Not Only SQL"
Não precisam de um schema fixo, não usam junções, e relaxam uma ou mais das propriedades ACID de BDs:

**ACID:**
- *Atômica*: Ou faz tudo, ou não faz nada.
- *Consistência*: Uma transação tem que não pode mudar outras coisas no BD.
- *Isolamento*: Controle de concorrência, duas transações não podem interferir uma a outra.
- *Durabilidade*: Mudanças por transações efetivadas devem persistir sem importar falhas.

Teorema **CAP**:
- *Consistência*:
- *Alta disponibilidade*:
- *Partição*:



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
.
.
.
.
.
.
.