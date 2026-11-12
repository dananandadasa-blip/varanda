# Varanda

Uma skill para transformar métricas de rede social em decisão — em português do Brasil, sem
jargão, sem relatório de duzentas páginas.

Ela não se conecta sozinha na sua conta. Você entrega os números (CSV exportado, export oficial,
print do painel ou um MCP que você já conectou), e ela calcula, interpreta e diz o que mudar.

Quer ver o caminho inteiro num desenho? Abra [`docs/mapa.html`](docs/mapa.html) no navegador: é uma página ilustrada, feita para quem nunca usou uma skill.

## O que ela faz

1. **Recebe os números** que você exporta do painel ou transcreve de um print — Instagram, TikTok,
   YouTube, LinkedIn, Facebook.
2. **Interpreta** o que cada índice significa, comparando com a sua própria média.
3. **Aponta o que melhorar**, com passo a passo e o número que prova se funcionou.
4. **Pesquisa tendências** dentro do seu contexto, com filtro de aderência.
5. **Escreve e reescreve roteiros** em linguagem simples e midiática — de 30 a 45 segundos.

Funciona em agente que leia o padrão `SKILL.md` — DeepSeek Harness, Claude Code, Codex, Cursor e
outros — desde que ele tenha o que cada trabalho pede:

| Para | O agente precisa |
|---|---|
| Qualquer análise com número | Rodar código (Python ou equivalente) e gravar arquivo |
| Ler print do painel | Modelo que lê imagem |
| Pesquisar tendência | Busca na web |

Sem um deles, a skill diz o que falta e não entrega aquele trabalho. Ela não faz conta de
cabeça nem cita fonte de memória. A saída é sempre em português.

## Por que existe

Painel de rede social mostra número, não mostra decisão. E conselho genérico de "poste mais e com
mais qualidade" não paga a conta.

A varanda faz três escolhas raras num painel:

- calcula em vez de estimar, e marca cada afirmação como `[medido]`, `[provável]` ou `[chute]`;
- compara com a **sua** média, não com benchmark de plataforma;
- termina em **um experimento com critério definido antes**, e começa a próxima rodada dando o
  veredito dele.

## Instalação sem terminal

O caminho mais curto. Não precisa de git nem de comando nenhum.

1. No repositório, clique em **Code → Download ZIP**.
2. Descompacte. Aparece uma pasta chamada `varanda-main`. **Renomeie para `varanda`.**
3. Vá até a pasta do seu workspace (a pasta do projeto onde você conversa com o agente) e entre
   em `.dsh/skills/` para DeepSeek Harness, ou `.claude/skills/` para Claude Code. Se `skills`
   não existir, crie.
4. Mova a pasta `varanda` para dentro.
5. Confira o caminho final. Ele tem que terminar assim:

```text
.../.dsh/skills/varanda/SKILL.md
```

Se o `SKILL.md` estiver um nível acima ou abaixo, a skill não carrega. Esse é o erro mais comum.

6. Abra uma sessão nova e digite `/varanda`. Se o agente responder chamando a skill, está
   instalada.

## Instalação com terminal

Se você já vive no terminal e prefere clonar:

```powershell
# DeepSeek Harness — rode dentro da pasta do seu workspace
git clone https://github.com/dananandadasa-blip/varanda .dsh/skills/varanda
```

```bash
# Claude Code
git clone https://github.com/dananandadasa-blip/varanda ~/.claude/skills/varanda

# Qualquer agente com o padrão Agent Skills
git clone https://github.com/dananandadasa-blip/varanda .agents/skills/varanda
```

Ou, pelo CLI de skills:

```bash
npx skills add dananandadasa-blip/varanda
```

Se o CLI não reconhecer o repositório (o `SKILL.md` fica na raiz, sem pasta `skills/`), use a
instalação sem terminal — o resultado é o mesmo.

## Como ela recebe seus números

Não existe login nem conexão automática. Quatro caminhos:

1. **Export oficial do Instagram.** Configurações → Sua atividade → Baixar suas informações.
   Escolha "Algumas informações", marque só Conteúdo e Insights, formato JSON, 30 dias. Vem um
   ZIP; ela tira de dentro só os arquivos de conteúdo e insights e transforma em tabela. (Caminho
   conferido em 2026-11; a Meta muda esse menu.)
2. **CSV do painel.** No Instagram, sai pelo Meta Business Suite, no navegador, e exige conta
   profissional. É o formato mais limpo.
3. **Print do painel.** Funciona. Ela lê a imagem uma vez, transcreve os números e trabalha por
   eles.
4. **MCP conectado** (por exemplo, Metricool). Se você já tem, ela puxa sozinha.

Sem nenhum dos quatro, ela faz uma leitura qualitativa e diz que é qualitativa. Não inventa número.

Dois avisos honestos:

- **Conta profissional é pré-requisito** para ver a maior parte desses números no Instagram.
- **Menos de 5 posts não é tendência.** É anedota, e a skill diz isso na cara em vez de fingir
  que dá para concluir algo.

O export completo do Instagram também traz suas mensagens diretas e seus contatos. A skill foi
instruída a trabalhar só com os arquivos de conteúdo e insights e a dizer o que deixou de fora —
mas prefira escolher "Algumas informações" e marcar só o que interessa.

## E se faltar um número que só aparece na tela?

Ela pede autorização. Em uma frase, e espera resposta antes de abrir qualquer página:

> Esse número só aparece no painel. Se você quiser, eu abro a página com a sua autorização e leio
> a tela. Autoriza?

Autorizado, lê e transcreve. Nunca publica, apaga, impulsiona ou altera nada, e a autorização vale
para aquela leitura — não fica valendo para sempre.

## Primeiro uso

```
/varanda analise essas métricas
```

Na primeira conversa ela faz três perguntas — o que você publica, para quem, o que quer que
aconteça — e grava `metricas/perfil.md`. Depois pede o dado do período.

## O que ela cria na sua pasta

```text
metricas/
├── perfil.md                   público, objetivo, tom, números de partida
├── historico.md                uma linha por rodada + experimento aberto
├── dados/                      export cru, como veio
└── diagnosticos/AAAA-MM-DD.md  o relatório completo de cada rodada
```

Tudo em texto, na sua máquina, em caminho relativo. A skill não guarda nada em servidor nenhum.
Se a sua pasta de trabalho é um repositório git, ponha `metricas/` no `.gitignore` dela antes do
primeiro uso: são dados da sua conta, e o `.gitignore` que vem com a skill não protege a sua
pasta.
O que você colar na conversa, porém, segue o caminho de qualquer mensagem: vai para o provedor do
modelo. Trate seus números como trataria um print no chat.

O relatório completo fica num arquivo `.md` dentro de `metricas/diagnosticos/`. Ele não aparece
sozinho na conversa: você abre quando quiser o detalhe. A resposta no chat são seis linhas.

## O que ela não faz

Isso importa mais que a lista de recursos:

- **Não vê sua conta sozinha.** Sem arquivo, print, MCP ou uma autorização sua para abrir a tela,
  ela não lê nada.
- **Não publica.** Nada é postado, agendado ou apagado. Só texto e arquivo.
- **Não promete viralizar.** O que dá para prometer é teste com critério, não resultado.
- **Não decide preço, oferta nem posicionamento.** Quando a causa é o negócio e não a métrica, ela
  diz isso e para.
- **Não substitui o painel.** Retenção de Reels, alcance de não-seguidores e dados de story muitas
  vezes só existem lá: você puxa, ela interpreta.

## O aviso `ATENÇÃO AQUI!`

Uma das regras da skill: **um aviso por resposta, só quando o gatilho acontece de verdade.** Ele
existe para você não se perder e não gastar contexto à toa.

```text
ATENÇÃO AQUI!
Esta conversa já tem três análises e ficou pesada.

1. Abra uma sessão nova.
2. Cole esta linha:

/varanda continue de metricas/diagnosticos/2026-11-10.md
```

Sempre no fim da resposta, no máximo dois passos, uma frase de motivo sem culpa, e uma linha
pronta para copiar. Nunca pede para você lembrar de nada.

Gatilhos, em ordem de prioridade: pedido de garantia de viral, tabela colada crua, pedido vago,
conversa pesada, comparação longa com perfil sem números de partida.

## Estrutura

```text
varanda/
├── SKILL.md                 o fluxo, as regras e o aviso
├── CHANGELOG.md             o que mudou em cada versão
├── references/
│   ├── entrada.md           o que pedir, o que aceitar, o que fazer sem dado
│   ├── metricas.md          dicionário de índices, fórmulas e faixas
│   ├── diagnostico.md       método para chegar à causa provável
│   ├── plano.md             do diagnóstico ao experimento
│   ├── trends.md            pesquisar tendência sem virar refém dela
│   ├── roteiro.md           escrever e reescrever para ser entendido
│   └── prompts.md           15 pedidos prontos
└── assets/
    ├── perfil.md            modelo de perfil
    └── historico.md         modelo de histórico
```

## Licença

MIT. Use, copie, adapte, publique. Se mudar algo que funcione melhor, mande de volta.
