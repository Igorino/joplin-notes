# Roteiro do vídeo

Duração alvo: 5 minutos, com margem. O texto das falas está escrito do jeito que se
fala, não do jeito que se escreve. As linhas de tela são instrução de gravação e não
devem ser lidas em voz alta.

## Orçamento de tempo

O roteiro tem 759 palavras faladas. A 155 palavras por minuto, que é ritmo de conversa,
isso dá 4 minutos e 54 segundos. A margem ficou pequena (6 segundos), porque o bloco 2
cresceu quando a demonstração da regra SWRL passou a precisar de um corte pro terminal
(ver a seção "Antes de gravar"). Por segurança, aplique já o corte 2 da tabela do final
antes de gravar, que devolve 8 segundos sem tirar nada essencial.

Vale um teste antes de gravar: leia o bloco 2 em voz alta cronometrado. Se ele passar de
1 minuto e 55 segundos, seu ritmo está abaixo de 155, e aí aplique também o corte 1.

| Bloco | Assunto | Entra em | Duração | Palavras |
|---|---|---|---|---|
| 1 | Problema e abordagem | 0:00 | 0:20 | 55 |
| 2 | Ontologia e reasoner ao vivo | 0:20 | 1:55 | 271 |
| 3 | Arquitetura | 2:15 | 0:20 | 44 |
| 4 | Recomendação e métrica | 2:35 | 1:00 | 152 |
| 5 | Cold start | 3:35 | 0:25 | 60 |
| 6 | Cadastro e SPARQL | 4:00 | 0:45 | 109 |
| 7 | Limitações e fechamento | 4:45 | 0:25 | 68 |

A duração de cada bloco já inclui o tempo de tela sem fala. A tabela soma 5 minutos e 10
segundos: aplicando o corte 2 (8 segundos) o vídeo cabe em 5:02, e aplicando também o
corte 1 (10 segundos) sobra folga de verdade, em 4:52.

## Antes de gravar

- Rodar `python scripts/verificar_ambiente.py` e esperar `Ambiente consistente.` Se a
  IDE tiver recriado o ambiente virtual, o Streamlit quebra no meio da demonstração.
- Apagar `dados/amazing.sqlite3` e subir o Streamlit **antes** de começar a gravar. A
  carga inicial leva de 5 a 15 segundos, que não cabem em um vídeo de 5 minutos. Deixar
  a aba do navegador aberta na tela de recomendações, com o João selecionado.
- Deixar o Protégé aberto com `ontologia/amazing-video.ttl` carregado e o reasoner
  **desligado**. O momento de ligar é ao vivo, e é o ponto alto do vídeo.
- Rodar `pytest` em um terminal e deixar a saída visível na tela, para usar no bloco 7
  sem gastar os 16 segundos de execução.
- Rodar `python scripts/validar_ontologia.py` em outro terminal e deixar a saída visível,
  para usar no bloco 2 na parte da regra SWRL. Esse script roda o Pellet de verdade; o
  Protégé mostra só a regra, não o resultado.

---

## Bloco 1. Problema e abordagem (0:00 a 0:20)

**Tela:** slide com o nome do trabalho.

**Fala:**

> A Amazing Video quer recomendar filme pros usuários dela.
>
> Dá pra fazer isso por conteúdo, olhando o que a pessoa declarou, ou por comportamento,
> olhando quem tem gosto parecido com ela. Só que o primeiro nunca surpreende, e o
> segundo não funciona com usuário novo.
>
> Eu misturei os dois, em cima de uma ontologia OWL.

---

## Bloco 2. Ontologia e reasoner ao vivo (0:20 a 2:05)

Este é o bloco mais importante. Se o vídeo estourar, corte em outro lugar.

**Tela:** Protégé, aba *Entities*, árvore de classes.

**Fala:**

> Essa é a ontologia: nove classes de topo, todas disjuntas entre si.
>
> Olha embaixo de Filme. Documentário é uma classe asserida, normal. Já Filme Ficcional
> e Filme Premiado têm um símbolo diferente, porque elas são classes definidas: elas não
> dizem o que o filme é, elas dizem uma condição. Quem decide é o reasoner.

**Tela:** clicar em `FilmePremiado`, mostrar o painel *Equivalent To*.

**Fala:**

> Filme Premiado é todo filme que ganhou pelo menos um prêmio. Ninguém escreve isso no
> arquivo. O sistema deduz.

**Tela:** clicar em `pulpFiction`, na aba *Individuals*, com o reasoner ainda desligado.

**Fala:**

> Esse é o Pulp Fiction, com o reasoner desligado: só Filme.

**Tela:** menu *Reasoner*, HermiT, *Start reasoner*. Voltar em `pulpFiction`.

**Fala:**

> Ligando o reasoner.
>
> Pronto. Agora ele é Filme Ficcional e Filme Premiado, os dois em amarelo, que é como o
> Protégé marca o que foi inferido. Premiado porque ganhou o Oscar de roteiro, ficcional
> porque não é documentário. Eu não escrevi nenhum dos dois.

**Tela:** clicar em `bowlingForColumbine`.

**Fala:**

> E aqui tá a parte mais interessante. O enunciado diz que todo filme precisa de diretor
> e de ator, menos documentário, que tem só diretor.
>
> Esse aqui é documentário: a lista de atores dele tá vazia, e ele não aparece como
> Filme Ficcional. Como a exigência do ator tá pendurada em Filme Ficcional, e não em
> Filme, o documentário escapa dela sem gerar contradição. A exceção virou axioma, não
> virou "if" no código.

**Tela:** aba *Rules*, mostrar a regra SWRL.

**Fala:**

> Tem uma regra SWRL também: se o usuário gosta de um ator, os gêneros dos filmes desse
> ator viram preferência dele.
>
> O HermiT daqui do Protégé não roda SWRL. Quem materializa essa regra é o Pellet, que é
> o reasoner que o sistema usa por trás.

**Tela:** trocar para o terminal com a saída do `validar_ontologia.py` já rodada, apontar
pra linha "prefereGenero de carlos apos a regra SWRL".

**Fala:**

> O Carlos declarou só Ação, Crime e Keanu Reeves. Depois do Pellet rodar, ele também
> prefere Ficção Científica, porque o Keanu tá em Matrix.

---

## Bloco 3. Arquitetura (2:05 a 2:20)

**Tela:** editor com a estrutura de pastas, ou um slide com a lista.

**Fala:**

> A stack é Python com Owlready2, que me dá o acesso à ontologia, o quadstore e o
> SPARQL. O reasoner é o Pellet, que é o que materializa SWRL, e a interface é
> Streamlit. Não tem banco relacional: é RDF do começo ao fim.

---

## Bloco 4. Recomendação e métrica (2:20 a 3:15)

**Tela:** navegador, tela de recomendações, João selecionado.

**Fala:**

> Esse é o João, que já avaliou cinco filmes. A primeira tela que ele vê já é a lista
> pronta.
>
> No topo vem Matrix, com previsão de 4,1 estrelas, e o item explica por que ele entrou:
> o João curte Ação, o filme é premiado, e o Bruno, que tem gosto parecido com ele, deu
> nota alta. Essas três razões vêm de lugares diferentes: do que ele declarou, da classe
> que o reasoner inferiu, e do cálculo de similaridade.

**Tela:** apontar para a linha de números.

**Fala:**

> Esse alfa aqui é o coração da métrica: é três dividido por três mais o número de
> avaliações da pessoa. O João tem cinco, então dá 0,375: 37% de conteúdo e 63% de
> social. Quanto mais ele avalia, menos o sistema depende do que ele declarou.

**Tela:** "Avaliar filme", Matrix, nota 1, gravar. Voltar em "Recomendacoes".

**Fala:**

> Vou dar uma estrela pro Matrix. Pronto, ele saiu da lista, porque filme já visto não
> se recomenda. E foi instantâneo, porque avaliar não roda o reasoner.

---

## Bloco 5. Cold start (3:15 a 3:40)

**Tela:** trocar o usuário para Diego Ramos.

**Fala:**

> Agora o caso difícil: o Diego acabou de se cadastrar e não avaliou nada. O alfa dele é
> 1,00, cem por cento conteúdo, porque ele não tem vizinho nenhum.
>
> E mesmo assim o sistema recomenda, marcando cada item como "baseado apenas em
> conteúdo". Não teve divisão por zero: sem vizinho, o componente social fica
> indefinido, e indefinido não é zero.

---

## Bloco 6. Cadastro e SPARQL (3:40 a 4:30)

**Tela:** "Cadastro de filme", título "Filme Sem Elenco", diretor preenchido, Atores em
branco. Enviar.

**Fala:**

> Se eu tentar cadastrar um filme ficcional sem ator, ele bloqueia e explica o motivo.
> Essa validação tá na aplicação, e não no reasoner, porque em mundo aberto o reasoner
> ia concluir que existe algum ator que eu não informei.

**Tela:** cadastro válido, "Duna", com Nome do prêmio e Evento preenchidos. Enviar.

**Fala:**

> Agora um cadastro válido, com prêmio. Olha a linha de baixo: Filme Ficcional inferido,
> Filme Premiado inferido. Eu não marquei nenhum dos dois.

**Tela:** "Explorar catalogo", "Listagem combinada", gênero Drama e nacionalidade Brasil.
Abrir o painel "SPARQL gerado".

**Fala:**

> Nas listagens: Drama e Brasil, três filmes. Esse painel mostra o SPARQL que foi
> montado, só com os filtros que eu preenchi.

**Tela:** marcar "Somente filmes premiados" e limpar os outros filtros.

**Fala:**

> E esse filtro aqui consulta a classe Filme Premiado. Sem o reasoner, essa lista vinha
> vazia, porque nenhum filme é declarado premiado no arquivo.

---

## Bloco 7. Limitações e fechamento (4:30 a 5:00)

**Tela:** terminal com a saída do `pytest` já visível.

**Fala:**

> Pra fechar, o que o trabalho não faz. A base de avaliação é sintética: 37 notas de 7
> usuários. Com base pequena o Pearson fica instável, e os pesos da métrica foram
> escolhidos por julgamento, não calibrados.
>
> O que dá pra afirmar é o que foi verificado: ontologia consistente, classes definidas
> inferidas sem asserção na mão, a regra SWRL disparando, e os 132 testes passando.
>
> É isso. Obrigado.

---

## Se estourar o tempo

Cortar nesta ordem, do primeiro para o último:

| Ordem | O que cortar | Ganho |
|---|---|---|
| 1 | No bloco 6, a explicação de mundo aberto, deixando só "ele bloqueia e explica o motivo" | 10 s |
| 2 | No bloco 4, a frase das três origens da explicação | 8 s |
| 3 | O bloco 3 inteiro, deixando a arquitetura só para o relatório | 17 s |
| 4 | No bloco 4, a frase "E foi instantâneo, porque avaliar não roda o reasoner" | 3 s |

Os quatro cortes somam 38 segundos.

Não cortar do bloco 2. A inferência ao vivo e a exceção do documentário são o que
diferencia o trabalho de um sistema de recomendação sem ontologia.

## O que ficou de fora

Estes pontos estavam na versão de 12 minutos e saíram por tempo. Todos estão
documentados, e servem de resposta caso sejam perguntados na arguição.

| Assunto | Onde está |
|---|---|
| IRI determinística da avaliação, que evita duplicata ao reavaliar | `docs/relatorio.md`, seção de CRUD, e passos 13 e 14 do `docs/manual.md` |
| Separação entre grafo asserido e grafo inferido | `docs/relatorio.md`, seção de arquitetura |
| Axiomas de fechamento, e por que eles são necessários sob mundo aberto | `docs/relatorio.md`, seção de decisões de modelagem |
| Erro de contradomínio de `sobreFilme` na Fase 1 | `docs/relatorio.md`, e o teste que reproduz a inconsistência em `tests/test_ontologia.py` |
| Ponderação por significância no Pearson | `docs/relatorio.md`, seção da métrica |
| Os quatro arquivos de `src/`, e por que o recomendador não conhece o Owlready2 | `docs/relatorio.md`, seção de arquitetura |
