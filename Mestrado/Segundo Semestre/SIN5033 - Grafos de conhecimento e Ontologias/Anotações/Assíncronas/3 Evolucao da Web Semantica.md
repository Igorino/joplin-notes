# Linha do tempo
De onde viemos até os Grafos de Conhecimento:
- **1945** - Memex, o precursor de tudo.
	- **Vannevar Bush** imaginou o Memex: uma máquina que daria acessos a grande coleções de texto via trilhas de links e anotações, não dissemelhante à internet moderna e seus hiperlinks. Nunca foi construido, mas plantou a semente do hipertexto.
- **1965** - Primeiras conexões:
	- **Ted Nelson** pensou em uma organização de objetos de forma altamente conectada. Elementos: **nós** (pedaços de texto) + **hiperlinks** (conexões lógicas entre nós). Na época, foi conceptualizado com apenas texto, sem multimídia.
- **1980s** - Hipermídia:
	- Na década de 1980, começa-se a pensar em uma evolução do hipertexto: com recursos multimídia (imagens, vídeo, audio, etc.) que passam a fazer parte da estrutura ligada de nós. Ainda não tem a semântica.
- **1990** - Hipermídia posta em prática:
	- **Tim Berners-Lee** conceptualiza um sistema de hipermídia exemplar, proposto no CERN (Sim, aquele CERN mesmo, do acelerador de partículas, que é só mais um dos seus projetos relacionados a pesquisa nuclear). Combina **URI** (Identidade) + **HTTP** (comunicação) + **HTML** (representação). Os links entre documentos não são tipados, a máquina *não sabe* por que A aponta para B.
- **2001** - :
	- **Berners-Lee**, **Hendler** e **Lassila** pensam em uma visão "top-down", "de cima para baixo": anotar o conteúdo existente com significado formal via ontologias (OWL, RDFS). Foco em *raciocínio automático*. Grandes resultados em medicina/biologia (Gene Ontology, SNOMED CT, etc.). Mas criar ontologias é caro e complexo demais.
- **2006** - Dados Ligados (Linked Data):
	- Pensam em uma bordagem "bottom-up", "de baixo para cima": publicar dados estruturados usando URIs + RDF + HTTP, ligando conjuntos de dados entre si. Ênfase na *interoperabilidade*, não necessariamente na *riqueza ontológica*. Muito mais fácil e barato de aplicar em larga escala.
- **2012** - Grafos de Conhecimento e Google:
	- Em 2012, a Google populariza o termo com o seu *Knowledge Graphs* baseado no [schema.org](schema.org). Diferença principal: GCs são *internamente consistentes e controlados* (indústria). Eles não são abertos como o projeto da LOD Cloud. A Microsoft, IBM, Facebook e eBay adotam o conceito. Ele também tem forte ligação com os conceitos de Machine Learning e Deep Learning.
- **Hoje** - Convergência da Web Semântica com Linked Data e GC:
	- Hoje os três pilares convivem: **Ontologias** servem para fornecer o *vocabulário formal*; **Linked data** serve para publicar e conectar os dados; Enquanto **Grafos de Conhecimento** estruturam o conhecimento para aplicações industriais e de IA.

# A virada central
A web que hoje nós conhecemos é uma **web de documentos**: HTML é usado para fazer a sua *estrutura visual*, HTTP é usado para *comunicação* e URI é usado para fazer o *endereçamento*. Os *hiperlinks* ligam as páginas, mas não dizem o **porquê**. A máquina não sabe se o link é "é autor de", "trabalha em" ou "contradiz" o conteúdo! Isso é problema dos enlaces (ou ligações) não tipados.

A Web de Dados se propõe a resolver isso trocando os *documentos* por *coisas*, e *hiperlinks genéricos* por *enlaces tipados em RDF*. 

```mermaid
