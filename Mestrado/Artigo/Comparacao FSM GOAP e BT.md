# Comparação FSM, GOAP e BT

Sugestão de protocolo experimental para a qualificação.

## Passo 1. Escrever o que quero descobrir
- Definir a pergunta: qual das três técnicas (FSM, GOAP, BT) entrega o melhor equilíbrio entre parecer convincente e não pesar no PC
- Anotar o que espero antes de rodar, pra não ficar "achando" depois

## Passo 2. Montar um cenário único de teste
- Usar um só mapa e uma só situação (ex.: o NPC patrulha e reage quando me vê)
- Rodar exatamente o mesmo cenário em todas as versões, senão a comparação não vale

## Passo 3. Fazer as três versões do NPC
- Manter o mesmo comportamento por fora (patrulhar, perceber, perseguir)
- Trocar só o "motor" de decisão por dentro (FSM, GOAP, BT)
- Deixar o resto igual (velocidade, mapa, física) pra isolar a técnica

## Passo 4. Escolher o que vou mexer
- Variar o alcance da visão do NPC em 2 ou 3 níveis (curto, médio, longo)
- Testar cada técnica em cada nível, sempre do mesmo jeito

## Passo 5. Definir o que meço no PC
- Medir uso de CPU
- Medir uso de memória
- Medir o tempo que o NPC leva pra decidir
- Medir o FPS do jogo
- Coletar isso automático durante cada rodada, várias vezes, pra tirar média

## Passo 6. Definir como sei se parece convincente
- Pedir pra algumas pessoas jogarem e responderem um questionário curto
- Basear as perguntas em critérios já prontos da literatura (não inventar do zero)
- Ligar "o que o jogador sente" com "o que o PC mostra"

## Passo 7. Rodar os testes de forma organizada
- Montar uma tabela com todas as combinações (técnica x nível de visão)
- Rodar cada combinação o mesmo número de vezes
- Salvar tudo com nome claro pra não se perder depois

## Passo 8. Comparar e escrever
- Juntar os números e ver quem gastou menos e quem convenceu mais
- Mostrar os trade-offs (ex.: GOAP convence mais mas pesa mais)
- Ligar isso de volta na pergunta do Passo 1