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