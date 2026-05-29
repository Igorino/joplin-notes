# Tese central
- A escolha de arquitetura de NPC é um posicionamento em trade-offs entre quatro eixos:
	- **Custo computacional / escalabilidade**;
	- **controlabilidade / autoria**;
	- **explicabilidade**; e
	- **comportamento emergente**.
- A pergunta poderia focar na tensão entre **emergência** e **explicabilidade**.
- **Explicabilidade** é o eixo que game AI quase nunca trata como critério. *(Pode ser minha contribuição?)*

# Ajuste sobre LLMs (ponto revisado)

- Dois argumentos contra LLM-por-NPC:
	- **Custo/escalabilidade**: latência e VRAM por agente, inviável em multidão. Vale para LLM.
	- **Explicabilidade/controle**: caixa-preta. Vale para LLM e pra NN.

Para rede neural pequena, sobra só a explicabilidade. (Não juntar "LLM" com "NN").

# Bibliografia

- Oito artigos:
	- **Lapeyrade** e **Studiawan**: ancoram planejamento e explicabilidade.
	- NPC engine (**Magnenat**): cruza emergência e inspeção da decisão.
	- **AlJammaz**: vocabulário de credibilidade ("behavior understandability").
	- **Silva & Ribeiro e Chen**: mapeiam o campo (SLRs).
	- Três fontes de escalabilidade, com **Gallotta et al**. (IEEE ToG) como âncora.

# A Lacuna

- Nenhuma fonte é sobre explicabilidade propriamente.
- Confirma que o ângulo é **subexplorado**.
- Falta buscar literatura de XAI e plan-explanation. Prioridade de leitura.

# Justificativa do recorte (BT/GOAP)

- Partir dos eixos.
- Argumento de viabilidade (custo).
- Argumento de projeto (controle/explicabilidade).
- Só se estuda explicabilidade em arquiteturas que a possuem, então devo focar em BT/GOAP(?)

# Demo em Godot

- Cérebros intercambiáveis (FSM, GOAP, Bayesiano, LLM) no mesmo cenário.
- Objetivo: tornar visível a diferença de explicabilidade entre eles?

# Artigos

| Nome do artigo | Resumo | Como ajuda a minha tese? |
| --- | --- | --- |
| **Zhu (2019): Behavior Tree + Q-learning em Unity3D** | Implementação BTs para NPCs em Unity e propõe um híbrido BT + RL. Foco em viabilidade e eficiência de execução (roda estável, baixo consumo). | **Sustentação fraca**. Exemplo de implementação de BT e de arquitetura híbrida (gancho para 'trabalhos futuros'). Fonte de baixo impacto. |
| **Silva & Ribeiro (2021, SBGames): SLR de comportamento crível** | Revisão sistemática (18 estudos) sobre NPCs com comportamento crível. Constrói taxonomia (decisão, emoção, papel) e aponta que técnicas tradicionais viram obstáculo: o designer perde "controle firme" das respostas conforme a complexidade cresce. | **Sustentação Forte**. Aliado metodológico, em português, no SBGames. Mapeia o campo e enuncia o eixo de controlabilidade. Fonte de mineração de referências canônicas (cita Colledanchise). |
| **Chen (2024): SLR de NPC behavior e DDA** | Tese de mestrado. Moldura 'AI tradicional x real AI', percorre regras/FSM/BT até RL/deep learning. Cita interpretabilidade como vantagem da AI tradicional e a tensão autonomia x intenção de design. | **Forte**. Serve de modelo de estrutura (é uma SLR de mestrado) e de moldura para o argumento contra NN. Também fonte de garimpo de referências. |
| **Nugraha et al. (2025): FSM em RPG Maker** | Implementa FSM (Patrol/Transition/Chase) com diálogo condicional. Mede tempo de resposta e uso de recursos. Recomenda explicitamente **estudo comparativo FSM x BT x AI**. | **Sustentação fraca**, e confirma a lacuna. A própria literatura pede o comparativo que posso fazer. *Citar de leve?* |
| **Magnenat et al. (2022): NPC engine, MCTS para narrativa emergente** | Framework multiagente, modular, em Rust, para "narrativa emergente". Suporta valor estimado por rede neural opcional e, principalmente, recursos de depuração como plotar a árvore de busca. | **Extremamente interessante**. Único que cruza vários dos eixos: planejamento, emergência, inspeção da decisão (árvore plotável = proto-explicabilidade) e multiagente.
| **Lapeyrade (2022): raciocínio com ontologias (Prolog/WFS)** | Propõe decisão de NPC via programação lógica e ontologias hierárquicas. Afirma que a abordagem lógica permite explicação fácil e completa do resultado, ao contrário de técnicas de aprendizado, útil para explicar o comportamento ao jogador. | O mais próximo da tese. Abre com os mesmos eixos (FSM/BT/Utility/Planning). Ataca NN pela opacidade/autoria. Conecta com sua disciplina de Ontologias. |
| **Studiawan et al. (2018): GOAP em jogo espacial** | 
| **AlJammaz, Wardrip-Fruin & Mateas (2023): Character Believability** |

## Artigos que abordam escalabilidade de LLMs
| Nome do artigo | Resumo | Como pode me ajudar? |
| --- | --- | --- |
| **Gallotta et al. (2024, IEEE Transactions on Games): Survey & Roadmap de LLMs em jogos** | Survey revisado por pares (autores incluem Togelius e Yannakakis). Mapeia os papéis de LLMs em jogos e discute limitações: **custo computacional em tempo real, sustentabilidade e direitos autorais** nos dados. | Âncora revisada do **eixo de escalabilidade**. Usar como base (mas não a do arXiv). Autores já citados no resto da bibliografia. Também mapeia papéis de LLM (serve à seção de arquiteturas). |
| **Echoes of Others (INLG 2025, faixa de demos): protótipo UE5 com back-ends intercambiáveis** | Protótipo em Unreal Engine 5 integrando três back-ends (GPT-4o Mini na nuvem, OpenHermes-7B e variante LoRA 4-bit), caracterizando o **trade-off velocidade × qualidade local × nuvem sob orçamento de 60 FPS**. | Reforço revisado (demo track). Precedente metodológico direto do demo de 'cérebros intercambiáveis'. Também tem números de custo. Infelizmente o escopo é só sobre diálogo. |
| **Andreasen & Esterle (2025, arXiv, PREPRINT)** | Mede latência e VRAM por NPC usando Small Language Models (SLMs), como DistilGPT-2, TinyLlama-1.1B, Mistral-7B, em "hardware de consumo". Mostra latência alta mesmo com divisão. | Evidência recente complementar. Referência legal, mas sem **revisão por pares** (não achei publicado). *Posso citar com ressalva?* Escopo também é só diálogo. |
