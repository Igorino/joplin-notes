# Plano de Revisão Sistemática (rascunho)
## Atualização do estado da arte em arquiteturas de comportamento de NPC em jogos digitais (De 2021 até o presente)

# 1. Motivação e justificativa

- A revisão sistemática de Silva & Ribeiro (SBGames 2021) mapeou o estado da arte de NPCs com comportamento crível
- Mas só com artigos até 2021.
- Período é anterior à popularização dos modelos generativos (ChatGPT, nov/2022) e ao marco dos agentes generativos (Park et al., 2023).
- O campo incorporou paradigmas que aquela revisão não pôde observar:
	- diálogo via LLM/SLM,
	- agentes generativos,
	- sistemas multi-agente e
	- arquiteturas híbridas.
	- etc.

- Autores não tiveram um artigo de seguimento/follow-up sobre o assunto depois de 2021.
- Aqui poderia se propor em **atualizar** aquele mapeamento, que foi documentando o quanto e como o estado da arte mudou no intervalo.

- **Mas ler através dos três eixos de trade-off** que orientam a escolha de uma arquitetura de NPC:
	1. **Custo computacional / escalabilidade**
	2. **Controlabilidade / autoria**
	3. **Comportamento emergente**

(*Controlabilidade* e *Explicabilidade* foi juntada por ocuparem o mesmo espaço dentro desse escopo de jogos digitais)

A hipótese de fundo (que veio da revisão de 2021) é que existe uma tensão entre esses eixos: entre **emergência** e **controle**.

# 2. Perguntas de pesquisa

**RQ1: Panorama Geral**
Quais arquiteturas de decisão/comportamento de NPC foram propostas ou aplicadas em jogos digitais desde 2021, e como elas se distribuem entre os paradigmas (simbólico/determinístico, baseado em aprendizado, generativo/LLM, multi-agente, híbrido)?

**RQ2: Custo/escalabilidade**
Quais custos computacionais e limites de escalabilidade são reportados para cada arquitetura (latência, memória/VRAM, custo por agente, viabilidade em multidão)?

**RQ3: Controlabilidade/autoria** 
Como cada arquitetura trata a autoria e o controle do designer sobre o comportamento do NPC (facilidade de testar, controlar e alterar; "controle firme" das saídas)?

**RQ4: Emergência vs. controle** 
Como o comportamento emergente é caracterizado e avaliado, e qual a relação/tensão entre emergência e explicabilidade/controle?

**RQ5: Credibilidade/percepção** 
Como a credibilidade (believability) e a percepção do jogador são avaliadas nesses trabalhos, e que métodos (inclusive de base psicológica) são empregados?

---

# 3. Estratégia de busca

- **Janela temporal:** 2021 até o presente.
- **Idiomas:** inglês e português.
- **Bases eletrônicas:**
	- ACM Digital Library
	- IEEE Xplore
	- Scopus
	- SpringerLink
	- Portal de Periódicos CAPES
	
- **Fontes de conferência/periódico específicas da área**:
	- SBGames (Simpósio Brasileiro de Jogos)
	- IEEE Conference on Games (CoG) / antiga COG
	- AIIDE (AAAI Conference on AI and Interactive Digital Entertainment)
	- FDG (Foundations of Digital Games)
	- ICAART
	- IEEE Transactions on Games (ToG)

**String de busca (modelo — ajustar a sintaxe por base):**

```
("non-player character" OR "non player character" OR NPC)
AND (game OR "video game" OR videogame OR "digital game")
AND (behavior OR behaviour OR "decision making" OR "decision-making" OR dialogue OR dialog)
AND ("finite state machine" OR FSM OR "behavior tree" OR "behaviour tree" OR GOAP
     OR "goal-oriented action planning" OR "utility AI" OR ontology
     OR "reinforcement learning" OR "large language model" OR LLM
     OR "small language model" OR SLM OR "generative agent" OR "multi-agent" OR "multiagent")
```

**String complementar para o eixo de explicabilidade** (rodada à parte, depois combinada):

```
(NPC OR "non-player character") AND (game OR "video game")
AND (explainability OR explainable OR interpretability OR interpretable
     OR "plan explanation" OR transparency OR "behavior understandability")
```

**Versão em português (essência):**

```
(NPC OR "personagem não jogável" OR "personagem não-jogável")
E (jogo OR "jogo digital")
E (comportamento OR "tomada de decisão" OR diálogo)
E (máquina de estados OR "árvore de comportamento" OR GOAP OR ontologia
   OR "aprendizado por reforço" OR "modelo de linguagem" OR LLM OR SLM
   OR "agente generativo" OR "multiagente" OR explicabilidade OR interpretabilidade)
```

# 4. Critérios de inclusão e exclusão

### **Inclusão (o trabalho deve satisfazer pelo menos um):**
- Apresenta arquitetura/técnica de decisão ou comportamento de NPC em jogos digitais.
- Reporta custo computacional, escalabilidade, controle/autoria, explicabilidade, emergência ou avaliação de credibilidade de NPCs.
- Propõe modelo, método, framework ou estudo comparativo aplicável a NPCs em jogos.

### **Exclusão:**
- Não satisfaz nenhum critério de inclusão.
- Trata exclusivamente de processos fora de escopo (pathfinding, geração procedural de conteúdo).
- Versão completa indisponível.
- Não está em inglês ou português.
- É editorial, resumo, workshop sem texto completo, vídeo ou tutorial.
- É versão anterior de um trabalho já considerado.

> A revisão de 2021 **excluiu** "serious games", que são educacionais. Pra manter coerência com o trabalho seria bom excluir eles também? Já que o contexto pode mudar entre educacionais e de entreterimento.

# 5. Critérios de qualidade

- O trabalho tem que passar por **revisão por pares** (duh)
- Apresentação, metodologia e validação coerentes.
- Responde a pelo menos uma das perguntas de pesquisa de forma objetiva.

# 6. Processo de seleção (funil)

1. Execução das strings nas bases $\rarr$ resultados brutos.
2. Remoção de artigos duplicados.
3. Triagem por título e resumo (critérios de inclusão/exclusão).
4. Leitura completa dos selecionados $\rarr$ aplicação dos critérios de qualidade.
5. Conjunto final de artigos.
6. Garimpo de referências (snowballing) a partir dos aceitos, para recuperar trabalhos-chave fora das bases.

> Funil faz parte da contribuição? 15-20 estudos é defensável?

# 7. Extração de dados

Pra cada estudo que passar pelo funil, pegar:
- Referência completa e publisher (e se é revisado por pares)
- Ano
- Paradigma da arquitetura (simbólico / aprendizado / generativo / multi-agente / híbrido).
- Eixo(s) tratado(s): custo, controle/autoria, explicabilidade, emergência, credibilidade, etc.
- Métricas reportadas (latência, memória, custo por agente, etc.).
- Forma de avaliação da credibilidade/percepção, se tiver.
- Engine/ferramenta.
- Mapeamento para RQ1 a RQ5.

> Montar uma planilha com uma linha por estudo e uma coluna por tipo de dado extraído? 

# 8. Referências-base já analisadas (ponto de partida pra snowballing)
- **Silva & Ribeiro (2021)**: Development of Non-player Character with Believable Behavior;
- **Lapeyrade (2022)**: Reasoning with Ontologies for Non-Player Character's Decision-Making in Games;
- **Lorandi & Belz (2025)**: Echoes of Others: Real-Time LLM Dialogue Generation for Immersive NPC Interaction;
- **Zhu (2019):** Behavior tree design of intelligent behavior of non-player character (NPC) based on Unity3D;

# 10. Referências com análise superficial
- **Studiawan et al (2018)**: Tactial Planning in Space Game using Goal-Oriented Action Planning;
- **Magnenat et al (2022)**: NPC engine: a High-Performance, Modular, and Domain-Agnostic MCTS Framework for Emergent Narrative;
- **Al Jammaz et al (2023)**: Torwards an Understanding of Character Believability;
- **Gallotta et al (2024)**: LLM and Games: A Survey and Roadmap;
- **Chen et al (2024)**: Literature review of Application of AI in improving gaming experience: NPC behavior and dynamic difficulty adjustment.
- **Park et al (2023)**: Generative Agents: Interactive Simulacra of Human Behavior

