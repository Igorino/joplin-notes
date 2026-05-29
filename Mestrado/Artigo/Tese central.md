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
	- **Explicabilidade/controle**: caixa-preta. Vale para LLM e para NN.

Para rede neural pequena, sobra só a explicabilidade. (Não juntar "LLM" com "NN").

# Bibliografia

- Oito artigos no corpus central, mapeados por função.
	- **Lapeyrade** e **Studiawan**: ancoram planejamento e explicabilidade.
	- NPC engine (**Magnenat**): cruza emergência e inspeção da decisão.
	- **AlJammaz**: vocabulário de credibilidade ("behavior understandability").
	- **Silva & Ribeiro e Chen**: mapeiam o campo (SLRs).
	- Três fontes de escalabilidade, com **Gallotta et al**. (IEEE ToG) como âncora.

# A lacuna

Nenhuma fonte é sobre explicabilidade propriamente.
Confirma que o ângulo é subexplorado (bom sinal).
Falta buscar literatura de XAI e plan-explanation. É a prioridade de leitura.

# Justificativa do recorte (BT/GOAP), em 4 movimentos

- Partir dos eixos, não das técnicas.
- Argumento de viabilidade (custo).
- Argumento de projeto (controle/explicabilidade).
- Só se estuda explicabilidade em arquiteturas que a possuem, então focar em BT/GOAP é condição da própria contribuição.

# Demo em Godot

- Cérebros intercambiáveis (FSM, GOAP, Bayesiano, LLM) no mesmo cenário.
- Objetivo: tornar visível a diferença de explicabilidade entre eles?

# Bibliografia

| Artigo | O que diz | Função no possível no trabalho |
| --- | --- | --- |
| Zhu (2019): Behavior Tree + Q-learning em Unity3D | Implementa BTs para NPCs em Unity e propõe um híbrido BT + Q-learning. Foco em viabilidade e eficiência de execução (roda estável, baixo consumo). | **Sustentação fraca**. Exemplo de implementação de BT e de arquitetura híbrida (gancho para 'trabalhos futuros'). Não usar como autoridade conceitual, pois é fonte de baixo impacto. |
| Silva & Ribeiro (2021, SBGames): SLR de comportamento crível | 