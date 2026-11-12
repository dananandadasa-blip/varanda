# Diagnóstico — do número à causa provável

> Revisado em 2026-11. O método não envelhece; a ordem dos sinais, sim (ver `metricas.md`).

Diagnóstico é uma frase que explica o padrão e admite o que não sabe.
Não é lista de observações.

## O método

0. **Dê o veredito do experimento aberto**, se houver um em `metricas/historico.md`, pelo
   critério escrito lá (regras em `plano.md`). Mova-o para "Experimentos encerrados".
1. **Calcule a base.** A base é uma só, para todo agente chegar ao mesmo número: a **mediana
   por post** de cada índice, sem os posts fora da curva (alcance acima de três vezes a mediana
   do período). Mostre ao lado a mediana com eles e a média, para quem quiser conferir. Não use
   taxa agregada (soma das interações ÷ soma do alcance) como base: um post grande domina.
   Por formato, só quando o formato tem 5 posts ou mais; abaixo disso, mostre os números e
   marque `[provável]`.
2. **Ordene pelo sinal principal da plataforma** (tabela em `metricas.md`), não por curtida.
   Se o dado não traz esse sinal, use o segundo e diga que trocou.
3. **Compare os melhores com os piores.** Com 10 posts ou mais, os cinco de cima contra os
   cinco de baixo. Com 5 a 9, a metade de cima contra a de baixo, e a conclusão é `[provável]`.
   O que muda entre os grupos é a hipótese.
4. **Isole uma variável.** Se os melhores são todos curtos, o padrão é duração. Se são todos de
   um tema, o padrão é tema. Se não há padrão, diga que não há.
5. **Escreva a hipótese em uma frase** e diga o que a derrubaria.

## As dimensões que costumam explicar

| Dimensão | Pergunta | Sinal de que é isso |
|---|---|---|
| Tema | Os melhores compartilham assunto? | O pior post é bom e o tema é que não puxa |
| Formato | Reel vence carrossel? | A diferença aparece dentro do mesmo tema |
| Gancho | Os melhores abrem com o quê? | Retenção inicial alta nos melhores |
| Duração | Curto vence longo? | Queda de retenção perto do fim |
| Horário | Há dia ou hora recorrente? | Padrão que se repete em semanas diferentes |
| CTA | Os melhores pedem algo? | Salvamento alto quando o post pede para salvar |

Se três dimensões mudaram juntas no período, não há diagnóstico — há confusão. Diga isso.

## Marcação obrigatória

- `[medido]` — saiu de conta sobre os dados.
- `[provável]` — inferência que se apoia em padrão observado.
- `[chute]` — hipótese sem apoio. Serve para testar, não para decidir orçamento.

Quem lê precisa saber onde está pisando. Um relatório que trata opinião como medição destrói a
confiança na segunda leitura.

## O que não dá para saber sem dado

Diga sempre que for o caso:

- Se o Reel foi entregue a quem não segue (a maioria dos painéis não separa).
- Se o story foi visto por seguidor ou por recomendação.
- Retenção por trecho, fora do YouTube.
- Quem salvou e quem comprou — atribuição de pessoa.
- Efeito de um post sobre a venda de duas semanas depois.

Fingir que sabe é pior do que admitir o buraco. O buraco vira pedido de dado.

## Formato do diagnóstico

```markdown
> Origem: <arquivo> · janela real <data> a <data> · denominador: <alcance ou visualizações>
> Colunas mapeadas: <nome no arquivo → campo>

## Veredito do experimento anterior

<confirmou, derrubou ou inconclusivo, com o número medido e o critério — ou "não havia
experimento aberto">

## Diagnóstico — <período>

**Base:** N posts (M fora da curva, de fora), mediana de X% de engajamento por <denominador>.
Com os fora da curva: mediana Y%, média Z%.

### O que subiu
<achado> [medido]

### O que caiu
<achado> [medido]

### Causa mais provável
<uma frase> [provável] — porque <evidência>.
O que derrubaria: <observação que mudaria a conclusão>.

### O que não dá para saber
<lista curta>

## Plano

<até três ações e o experimento — o conteúdo descrito em plano.md>

## Números por post

| Data | Formato | Dur. | Alcance | Eng. | Salv./1k | Comp./1k | Fora da curva |
|---|---|---|---|---|---|---|---|
| | | | | | | | |
```

Curto: fora a tabela por post, o relatório cabe em uma tela e meia.
Relatório longo não é lido, e o que não é lido não vira ação.
