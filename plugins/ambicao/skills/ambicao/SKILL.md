---
name: ambicao
description: "Reescreve um braindump ou pedido de tarefa num prompt mais ambicioso (altitude, profundidade e alcance), mostra o resultado e para antes de executar. Não copia para o clipboard. Use quando Marco invocar /ambicao ou pedir explicitamente a skill ambição (\"usa a ambição\", \"passa na ambição\"), inclusive por um coordenador que repassa o pedido dele. Não use por iniciativa própria."
argument-hint: "[braindump ou tarefa]"
---

# Ambição

Transforme o pedido de Marco num prompt melhor, não maior. Esta skill **não executa** a tarefa: ela devolve o prompt reescrito e para. Marco ajusta e manda executar ("vai"), ou pede para abrir numa sessão nova.

Base: o método de Felix Rieseberg em *How to be more ambitious: a tutorial for humans with models* (out/2026).

## Entrada

O texto após `/ambicao` é a tarefa ou o braindump: `$ARGUMENTS`. Se vier vazio, use a última mensagem de Marco ou o rascunho que ele indicar.

Antes de reescrever, recupere o contexto disponível na sessão: projeto, cwd, fontes, decisões já tomadas e restrições. Leia apenas o que muda a reescrita. Não comece a implementar nem a investigar o problema em si.

## Análise (curta, no chat)

Responda cada eixo em poucas linhas. Descarte o eixo que não melhora o resultado e diga isso em uma frase.

1. **Altitude.** O que Marco quer que aconteça depois que esta tarefa terminar? Existe um resultado durável acima da tarefa (por exemplo, "manter sem crashes" em vez de "corrigir este crash")? O que o agente precisaria ter (dados, acesso, ambiente de verificação) para cuidar desse resultado sem Marco alimentá-lo tarefa a tarefa? Em trabalho criativo, subir de nível costuma render pouco; diga quando for o caso.
2. **Profundidade.** O que um profissional de topo da área faria que o pedido não pede? De qual material mais cru ele partiria, em vez do que já veio digerido? Quais métodos e ferramentas ele usaria (banco de dados, modelo estatístico, profiler, reprodução real, em vez de tabela markdown)? Que premissa de Marco vale testar adversarialmente contra os dados brutos? Há uma meta ousada e específica que substitua "faça o melhor possível"?
3. **Alcance.** Reescreva o objeto da tarefa como verbos (não "um deck", mas "fazer gente ocupada decidir sob incerteza em 30 minutos"). Que outras áreas contribuem para esses verbos? Monte a equipe, incluindo quem atacaria o resultado. Use as áreas para escolher **técnicas**, nunca para role play: "faça o que um auditor forense faz", não "escreva como um auditor".
4. **Juiz externo.** O que, além do modelo e de Marco, mostra que o resultado está certo? Prefira algo que o agente consiga rodar e obter feedback imediato (teste, benchmark, dado não visto, reprodução, gate do projeto). Este item é obrigatório, mesmo quando os outros eixos forem descartados. Nunca aceite o modelo julgando o próprio trabalho como prova.

## Limites

- Preserve a intenção, o escopo autorizado e as decisões de produto de Marco. Ambição muda método, profundidade e critério de verificação; não amplia escopo nem toma decisões que são dele. Quando a versão mais ambiciosa exigir escopo novo, apresente como opção separada no fim.
- Respeite as instruções do projeto e o CLAUDE.md global: validação proporcional, sem CI durante a autoria, sem processo extra por rito.
- Se o pedido já estiver bem especificado e nada acima o melhora, diga isso e devolva o prompt quase intacto.
- Não narre a teoria do método no prompt final.

## Saída

1. A análise acima, enxuta.
2. O **prompt reescrito**, em PT-BR, num bloco de código, pronto para ser enviado como pedido de execução. Ele deve conter: objetivo e resultado esperado, material de partida e acessos, métodos esperados, meta concreta quando houver, premissas a testar, juiz externo e condição de término.
3. **Não copie para o clipboard.** Marco guarda coisas no Cmd+C e não pode perder. Entregue o prompt só no bloco do chat (ou em arquivo, se for longo). Use `pbcopy` apenas se Marco pedir a cópia explicitamente naquele momento.
4. Pare. Não execute a tarefa. Diga em uma linha que Marco pode responder "vai" para executar aqui ou pedir uma sessão nova, indicada quando o braindump é longo e a execução deve começar com o contexto limpo.

Se Marco pedir sessão nova, abra-a com o prompt reescrito como brief (contexto `fresh`), no projeto correspondente.
