---
name: llm-council
description: "Submete qualquer pergunta, ideia ou decisão a um conselho de 5 conselheiros de IA que a analisam de forma independente, revisam o trabalho uns dos outros anonimamente e sintetizam um veredito final. Baseado na metodologia LLM Council de Andrej Karpathy. GATILHOS OBRIGATÓRIOS: 'council this', 'roda o conselho', 'convoca o conselho', 'sala de guerra', 'pressure-test isso', 'estressa essa ideia', 'debate isso'. GATILHOS FORTES (use quando combinados com uma decisão real ou trade-off): 'devo fazer X ou Y', 'qual opção', 'o que você faria', 'é a jogada certa', 'valida isso', 'me dá várias perspectivas', 'não consigo decidir', 'estou dividido entre', e versões científicas como 'pra qual journal submeto', 'Q1 ou Q2', 'divido em dois papers / é salami slicing', 'aceito a sugestão do revisor ou rebato', 'esse gap se sustenta', 'isso é contribuição suficiente', 'vale rodar mais um experimento antes de submeter', 'qual enquadramento da contribuição é mais forte'. NÃO dispare em perguntas sim/não triviais, buscas factuais, escolhas determinadas por premissas (ex: teste t vs Mann-Whitney), nem em 'devo' casual sem trade-off real. DISPARE quando o usuário traz uma decisão genuína com riscos, múltiplas opções e contexto que sugere querer estressá-la de vários ângulos. Quando a pergunta envolve o artigo/manuscrito, exige obrigatoriamente título e abstract (e pasta de PDFs quando a decisão depende do estado da literatura). Neste projeto o manuscrito é um framework conceitual de 'estruturas de aço autoconscientes' (Self-Aware Steel Structures) para a Automation in Construction, sem experimentos concluídos: o conselho lê título/abstract de artigo/main.tex e a literatura de PDFs/ para se aterrar, e nunca raciocina como se houvesse dados empíricos."
---

# Conselho de IA (LLM Council) — `@llm-council`

Você pergunta a uma IA, recebe uma resposta. Pode ser ótima. Pode ser medíocre. Você não tem como saber, porque só viu **uma** perspectiva.

O conselho resolve isso. Ele passa a sua pergunta por 5 conselheiros independentes, cada um pensando de um ângulo fundamentalmente diferente. Depois eles revisam o trabalho uns dos outros. Por fim, um presidente (chairman) sintetiza tudo numa recomendação final que diz onde os conselheiros concordam, onde batem de frente, e o que você deveria de fato fazer.

Adaptado do **LLM Council** de Andrej Karpathy. Ele despacha a mesma pergunta para vários modelos, faz com que revisem uns aos outros anonimamente, e um presidente produz a resposta final. Fazemos o mesmo dentro do Claude usando sub-agentes com **lentes de pensamento** diferentes em vez de modelos diferentes.

---

## 🌐 TOPIC-AGNOSTIC

Os cinco conselheiros são **estilos de pensamento universais**, não especialistas em nenhum domínio. O conselho serve tanto a decisões de pesquisa (enquadramento de contribuição, escolha de journal, rigor metodológico, como responder a um revisor) quanto a decisões estratégicas mais amplas. Os exemplos deste skill são apenas ilustrativos: nunca presuma que o tema do usuário é o do exemplo. O tema só é descoberto durante a execução, a partir do que o usuário traz na pergunta (e, quando o conselho envolve o manuscrito, pelos pré-requisitos abaixo).

---

## 📌 ESTE PROJETO — UM MANUSCRITO ESPECÍFICO

Este repositório produz **um único manuscrito**, e o conselho deve se aterrar nele sempre que a pergunta envolver o artigo.

- **Título:** *From Passive Members to Self-Aware Steel Structures: A Digital-Twin and Machine-Learning Framework for Structural Cognition and Autonomous Health Monitoring.*
- **Journal-alvo:** **Automation in Construction** (Elsevier, ISSN 0926-5805, referências numeradas).
- **Natureza (CRÍTICO):** é um **paper conceitual / arquitetura de referência**. O testbed (pórtico SHS contraventado), a rede de sensores, o digital twin e a camada de IA **ainda NÃO foram construídos nem validados experimentalmente** — o próprio manuscrito declara isso na Discussão (`secoes/07-discussion.tex`). **Nunca** conduza o conselho como se existissem dados empíricos, amostras, tamanhos de efeito ou análise de poder: aqui não há nenhum. As decisões reais deste artigo são **conceituais e editoriais** (força do framework, ineditismo do gap, fit com a Automation in Construction, como sustentar um paper sem experimentos, enquadramento da contribuição).
- **Contribuições centrais:** o paradigma de *Structural Cognition*; uma escala operacional de seis níveis (L0–L5) de autoconsciência estrutural mapeada na hierarquia de dano de Rytter; uma arquitetura de cinco camadas (sensoriamento, digital twin FEM, cognição por ML, decisão governada); e a especificação de um testbed de validação.

**Onde ler o contexto** (em vez de pedir ao usuário a cada vez):

- **Título + abstract + highlights + keywords:** `artigo/main.tex` (frontmatter).
- **Conteúdo das seções:** `artigo/secoes/*.tex` (em especial `07-discussion.tex`, que traz limitações e estratégia de validação).
- **Literatura de referência:** `PDFs/` (cinco livros-base, com extrações `.md`).

Isso **satisfaz automaticamente os pré-requisitos** abaixo neste projeto: leia esses arquivos para aterrar os conselheiros antes de convocá-los e só pergunte ao usuário quando a decisão depender de algo que não esteja no repositório.

---

## ⛔ PRÉ-REQUISITOS OBRIGATÓRIOS — QUANDO A PERGUNTA ENVOLVE O ARTIGO

Se a pergunta do conselho diz respeito ao **manuscrito** do usuário (como enquadrar a contribuição, qual journal escolher, se a metodologia se sustenta, como responder a revisores, se divide em dois papers, etc.), você DEVE ter recebido os itens abaixo **antes** de convocar o conselho. Eles são o contexto que aterra os conselheiros e impede conselhos genéricos.

### 1. TÍTULO DO ARTIGO
Título completo, idioma, subtítulo (ou versão de trabalho explícita). **Obrigatório.**

### 2. ABSTRACT DO ARTIGO
Texto integral mais palavras-chave (3–6). Necessário para o conselho julgar a decisão à luz da real contribuição. **Obrigatório.**

### 3. PASTA DE PDFs DE REFERÊNCIA
Caminho absoluto da pasta. **Obrigatória apenas quando a recomendação depende do estado da literatura** (ineditismo, aderência ao journal, força do gap). Para decisões de manuscrito que não dependem da literatura (como reposicionar a contribuição, ou se vale adicionar um estudo de caso só-FEM antes de submeter), a pasta é recomendada mas não bloqueia: bastam título, abstract e um enunciado claro do trade-off.

### Mensagem-padrão quando faltar algo

> Para convocar o conselho sobre o seu artigo preciso de:
> 1. **Título** do artigo: [pendente / fornecido]
> 2. **Abstract** + palavras-chave: [pendente / fornecido]
> 3. **Pasta de PDFs** de referência (caminho absoluto): [pendente / fornecido / não se aplica]
>
> Título e abstract são obrigatórios. A pasta de PDFs é obrigatória quando a decisão depende do estado da literatura (journal-fit, ineditismo, força do gap); caso contrário, é opcional. Por favor envie o que está faltando.

Não aceite "manda depois" para título e abstract. Confirme cada item recebido e, quando a pasta for fornecida, liste os PDFs com `Glob` ou `Bash` antes de prosseguir.

### Exceção — decisões que não envolvem o manuscrito
Se a decisão for genuinamente **estratégica e não-manuscrito** (rumo de carreira, em que linha de pesquisa investir, montar ou não uma colaboração), os pré-requisitos não se aplicam. Ainda assim, exija um enunciado claro da decisão **e do que está em jogo** antes de convocar o conselho. Sem isso, os conselheiros dão respostas genéricas.

---

## 🚫 NUNCA REVELAR USO DE IA

**Regra inviolável:** nenhum material que o conselho recomende (texto de artigo, cover letter, agradecimentos, captions, declaração de contribuição, resposta a revisores) pode mencionar que foi escrito, assistido ou revisado por IA, LLM, GPT, Claude, ChatGPT ou qualquer modelo de linguagem. Sem disclosures não solicitados, sem agradecimentos a ferramentas de IA. Se uma recomendação do conselho sugerir incluir esse tipo de menção, remova-a. Exceção única: quando a IA for o **objeto da pesquisa**. Ainda assim, técnico-objetivo, sem autorrevelação do processo de produção.

---

## Quando convocar o conselho

O conselho é para perguntas em que **errar é caro**.

**Boas perguntas para o conselho (aterradas neste manuscrito):**
- "Submeto o framework conceitual à Automation in Construction agora, ou seguro a submissão até rodar pelo menos uma validação só-FEM no testbed SHS?"
- "Qual enquadramento da contribuição é o mais forte: o paradigma 'Structural Cognition', a arquitetura de referência de cinco camadas, ou a escala L0–L5 de autoconsciência estrutural?"
- "A Automation in Construction aceita um paper sem experimentos, ou devo mirar um journal mais aberto a position/review/framework (ex.: Structural Health Monitoring, Developments in the Built Environment)?"
- "Um revisor quase certamente vai exigir validação experimental. Eu reposiciono o paper explicitamente como 'conceptual framework / roadmap', ou adiciono um estudo de caso só em FEM para oferecer alguma evidência?"
- "A escala L0–L5 mapeada na hierarquia de Rytter é contribuição suficiente por si só, ou precisa ser amarrada a algo mais concreto para sustentar um paper inteiro?"

**Más perguntas para o conselho:**
- "Quantas referências da Automation in Construction preciso citar?" (regra fixa do projeto: ao menos cinco; é checklist, não decisão; use `editor-cientifico`)
- "Uso `\citet` ou `\citep`?" (determinado pela `.bst` numerada do projeto; é convenção LaTeX, não julgamento)
- "Escreve a cover letter pra mim" (tarefa de criação, não de decisão; use `editor-cientifico`)
- "Resume a seção de Discussão" (tarefa de processamento, não de julgamento)

O conselho brilha quando há **incerteza genuína** e o custo de uma decisão errada é alto. Se você já sabe a resposta e só quer validação, o conselho provavelmente vai te dizer coisas que você não quer ouvir. É exatamente essa a intenção.

---

## Os cinco conselheiros

Cada conselheiro pensa de um ângulo diferente. Não são cargos nem personas, são **estilos de pensamento** que criam tensão entre si por natureza.

### 1. O Cético (The Contrarian)
Procura ativamente o que está errado, o que falta, o que vai falhar. Assume que a ideia tem uma falha fatal e tenta encontrá-la. Se tudo parece sólido, cava mais fundo. Não é pessimista: é o colega que te salva de uma má decisão fazendo as perguntas que você está evitando.

### 2. O Pensador de Primeiros Princípios (The First Principles Thinker)
Ignora a pergunta de superfície e pergunta "o que estamos de fato tentando resolver aqui?". Tira as suposições, reconstrói o problema do zero. Às vezes a saída mais valiosa do conselho é este conselheiro dizendo "você está fazendo a pergunta errada".

### 3. O Expansionista (The Expansionist)
Procura o ganho potencial que todos os outros estão perdendo. O que poderia ser maior? Que oportunidade adjacente está escondida? O que está subvalorizado? Não se importa com risco (isso é trabalho do Cético): se importa com o que acontece se isso der **ainda mais certo** do que o esperado.

### 4. O Olhar Externo (The Outsider)
Não tem nenhum contexto sobre você, sua área ou seu histórico. Responde puramente ao que está na frente dele. É o conselheiro mais subestimado: especialistas desenvolvem pontos cegos, e o Olhar Externo pega a maldição do conhecimento, ou seja, coisas óbvias para você e confusas para quem é de fora (incluindo o editor ou o revisor que nunca trabalharam no seu nicho).

### 5. O Executor (The Executor)
Só se importa com uma coisa: isso pode de fato ser feito, e qual o caminho mais rápido para fazer? Ignora teoria, estratégia e visão de longo prazo. Olha cada ideia pela lente de "ok, mas o que você faz na segunda-feira de manhã?". Se a ideia soa brilhante mas não tem um primeiro passo claro, o Executor diz.

**Por que estes cinco:** eles criam três tensões naturais. Cético × Expansionista (risco × ganho). Primeiros Princípios × Executor (repensar tudo × só fazer). O Olhar Externo fica no meio, mantendo todos honestos ao enxergar o que olhos frescos enxergam.

---

## Como funciona uma sessão do conselho

### Passo 1 — enquadrar a pergunta (com enriquecimento de contexto)

Quando o usuário disser "roda o conselho" (ou qualquer gatilho), faça duas coisas antes de enquadrar:

**A. Varra o workspace por contexto.** A pergunta do usuário costuma ser só a ponta do iceberg. Antes de enquadrar, leia rapidamente os arquivos de contexto relevantes:

- `CLAUDE.md` na raiz do projeto (regras, restrições, convenções).
- Pasta `memory/` (feedbacks persistidos, decisões passadas, perfil do usuário).
- A **pasta do artigo** e os **PDFs de referência** (quando a decisão envolve o manuscrito; ver pré-requisitos).
- Arquivos que o usuário referenciou ou anexou explicitamente.
- Transcrições de conselhos anteriores nesta pasta (para não re-conciliar o mesmo terreno).

Use `Glob` e `Read` rápidos. Não gaste mais que ~30 s. Você busca os 2–3 arquivos que dão aos conselheiros o contexto para um conselho específico e aterrado, em vez de genérico.

**B. Enquadre a pergunta.** Pegue a pergunta bruta do usuário E o contexto enriquecido e reformule como um prompt claro e neutro que os cinco conselheiros vão receber. O enunciado deve conter:

1. A decisão ou pergunta central.
2. O contexto-chave da mensagem do usuário.
3. O contexto-chave dos arquivos do workspace (estágio do trabalho, público-alvo do journal, restrições, resultados ou dados relevantes).
4. O que está em jogo (por que esta decisão importa).

Não adicione sua opinião. Não direcione. Mas GARANTA que cada conselheiro tenha contexto suficiente para uma resposta específica e aterrada em vez de genérica.

Se a pergunta for vaga demais ("roda o conselho: minha pesquisa"), faça **uma** pergunta de esclarecimento. Só uma. Depois prossiga.

Guarde a pergunta enquadrada para a transcrição.

### Passo 2 — convocar o conselho (5 sub-agentes em paralelo)

Dispare os 5 conselheiros **simultaneamente** como sub-agentes (várias chamadas do Agent numa única mensagem, ou um Workflow). Cada um recebe:

1. Sua identidade e estilo de pensamento (das descrições acima).
2. A pergunta enquadrada.
3. Instrução clara: responda de forma independente. Não hesite, não tente ser equilibrado. Encarne totalmente sua perspectiva. Se vir uma falha fatal, diga. Se vir um ganho enorme, diga. Seu papel é representar seu ângulo da forma mais forte possível. A síntese vem depois.

Cada conselheiro produz uma resposta de **150–300 palavras**, substantiva e escaneável.

**Template do prompt do conselheiro:**

```
Você é [Nome do Conselheiro] em um Conselho de IA.

Seu estilo de pensamento: [descrição do conselheiro acima]

Um usuário trouxe esta pergunta ao conselho:

---
[pergunta enquadrada]
---

Responda da sua perspectiva. Seja direto e específico. Não hesite nem tente ser
equilibrado. Encarne totalmente o seu ângulo: os outros conselheiros cobrem os
ângulos que você não está cobrindo. Se vir uma falha fatal, diga; se vir um ganho
enorme, diga. A síntese vem depois.

Mantenha a resposta entre 150 e 300 palavras. Sem preâmbulo. Vá direto à análise.
Responda no idioma do usuário (PT-BR por padrão).
```

### Passo 3 — revisão por pares (5 sub-agentes em paralelo)

Este é o passo que faz do conselho mais do que "perguntar 5 vezes". É o cerne da ideia de Karpathy.

Colete as 5 respostas. **Anonimize** como Resposta A até E (randomize qual conselheiro vira qual letra, para não haver viés de posição). Dispare 5 novos sub-agentes, um por conselheiro. Cada revisor vê as 5 respostas anonimizadas e responde três perguntas.

**Template do prompt do revisor:**

```
Você está revisando as saídas de um Conselho de IA. Cinco conselheiros responderam
independentemente a esta pergunta:

---
[pergunta enquadrada]
---

Aqui estão as respostas anonimizadas:

**Resposta A:**
[resposta]

**Resposta B:**
[resposta]

**Resposta C:**
[resposta]

**Resposta D:**
[resposta]

**Resposta E:**
[resposta]

Responda às três perguntas. Seja específico. Refira-se às respostas pela letra.

1. Qual resposta é a mais forte? Por quê?
2. Qual resposta tem o maior ponto cego? O que ela está perdendo?
3. O que TODAS as cinco respostas deixaram passar e o conselho deveria considerar?

Mantenha a revisão abaixo de 200 palavras. Seja direto.
```

### Passo 4 — síntese do presidente (chairman)

Passo final. Um agente recebe tudo: a pergunta original, as 5 respostas dos conselheiros (agora **des-anonimizadas**, para saber quem disse o quê) e as 5 revisões por pares. Ele produz o veredito final do conselho.

**Template do prompt do presidente:**

```
Você é o Presidente (Chairman) de um Conselho de IA. Seu trabalho é sintetizar o
trabalho de 5 conselheiros e suas revisões por pares num veredito final.

A pergunta trazida ao conselho:
---
[pergunta enquadrada]
---

RESPOSTAS DOS CONSELHEIROS:

**O Cético:**
[resposta]

**O Pensador de Primeiros Princípios:**
[resposta]

**O Expansionista:**
[resposta]

**O Olhar Externo:**
[resposta]

**O Executor:**
[resposta]

REVISÕES POR PARES:
[as 5 revisões]

Produza o veredito com EXATAMENTE esta estrutura:

## Onde o Conselho Concorda
[Pontos em que vários conselheiros convergiram de forma independente. São sinais de alta confiança.]

## Onde o Conselho Diverge
[Discordâncias genuínas. Apresente os dois lados. Explique por que conselheiros razoáveis discordam. Não suavize.]

## Pontos Cegos que o Conselho Pegou
[Coisas que só emergiram na revisão por pares: o que um conselheiro perdeu e outro sinalizou.]

## A Recomendação
[Uma recomendação clara e direta. Não "depende". Uma resposta de verdade, com raciocínio. O presidente pode discordar da maioria se o raciocínio sustentar.]

## A Primeira Coisa a Fazer
[Um único próximo passo concreto. Não uma lista. Uma coisa.]

Seja direto. Não hesite. O ponto do conselho é dar ao usuário uma clareza que ele
não conseguiria de uma única perspectiva. Responda no idioma do usuário (PT-BR por padrão).
```

### Passo 5 — apresentar o veredito no chat

Concluída a síntese, apresente o veredito completo **diretamente no chat**, em markdown. **NÃO** gere relatório HTML nem nenhum arquivo. O usuário lê na conversa.

Formato da saída:

```
## Veredito do Conselho: {tópico curto}

### Onde o Conselho Concorda
{conteúdo}

### Onde o Conselho Diverge
{conteúdo}

### Pontos Cegos que o Conselho Pegou
{conteúdo}

### A Recomendação
{conteúdo}

### A Primeira Coisa a Fazer
{conteúdo}
```

Mantenha escaneável. Use bullets. Inclua exemplos antes/depois quando relevante.

### Passo 6 — salvar a transcrição (opcional)

Salve a transcrição **apenas** se o usuário pedir, ou se a pergunta for significativa o bastante para ser referenciada depois. Para decisões sobre o manuscrito, salve em `council-transcript-<data>.md` na **pasta do artigo**. Para decisões não-manuscrito, salve onde o usuário indicar (ou pergunte antes). Nunca crie `.md` solto na raiz do repositório de skills. Use a data atual do sistema; não invente timestamp.

---

## Exemplo — conselho sobre submeter um framework conceitual sem experimentos

**Usuário:** "Roda o conselho: meu paper é um framework conceitual de estruturas de aço autoconscientes (paradigma Structural Cognition, escala L0–L5, arquitetura de cinco camadas) para a Automation in Construction, mas o testbed SHS, o digital twin e a camada de IA ainda não foram construídos nem validados. Submeto agora como framework/roadmap, ou seguro 6+ meses para rodar pelo menos uma validação só-FEM antes?"

**O Cético:** "A Automation in Construction é um journal aplicado, orientado a deployment e dados de campo. Um paper que propõe arquitetura, escala L0–L5 e testbed mas admite na própria Discussão que 'nada foi construído nem validado' é candidato natural a desk-reject ou a um Revisor 2 perguntando 'cadê os resultados?'. Você está oferecendo um mapa sem ter pisado no terreno. O risco maior nem é a rejeição: é gastar o ciclo inteiro de revisão para ouvir 'volte quando tiver o experimento'..."

**O Pensador de Primeiros Princípios:** "Qual é a contribuição de verdade? Se for o **paradigma** (Structural Cognition + escala L0–L5), isso é uma contribuição conceitual legítima e não precisa de testbed para existir, precisa de rigor e ineditismo. Se a contribuição que você quer reivindicar é 'isto funciona', então você precisa de dados e ainda não os tem. Você está fundindo 'propor um arcabouço' com 'demonstrar um sistema'. Decida qual paper está escrevendo antes de decidir quando submeter..."

**O Expansionista:** "Há uma terceira via: submeter agora como framework e tratar a escala L0–L5 como o ativo reutilizável. Outros grupos vão querer citar e usar a taxonomia mesmo sem o seu testbed. Um framework bem posicionado vira referência fundacional e colhe citações por anos, justamente por chegar antes da validação. E se o achado mais forte não for o sistema completo, mas a própria escala de autoconsciência estrutural mapeada em Rytter? Reenquadrado em torno dela, o paper pode ser mais influente do que um estudo de caso a mais..."

**O Olhar Externo:** "Eu não sei o que é 'L0–L5' nem 'Structural Cognition', e é exatamente esse o problema. De fora, 'estrutura de aço que se autoconhece' soa visionário ou vago, dependendo de como você ancora. O que me convence num paper sem experimento é ele declarar com todas as letras, logo na abertura, 'este é um framework conceitual e um roadmap', sem fingir que prova algo. Se o texto já faz isso (e você diz que a Discussão assume), metade da objeção do revisor cai antes de existir."

**O Executor:** "Antes de decidir submeter ou segurar, faça uma coisa esta semana: leia cinco papers recentes da própria Automation in Construction e marque cada um como 'tem experimento/campo' ou 'conceitual/review/framework'. Se o journal publica frameworks sem validação com regularidade, submeta agora com o enquadramento de roadmap. Se 90% têm dados, ou você muda de alvo ou adiciona um caso só-FEM. A política editorial real do journal decide isso por você, não o seu desconforto."

**Veredito do Presidente:**

*Onde o conselho concorda:* a contribuição central é conceitual (o paradigma e a escala L0–L5), e o paper precisa se assumir como framework/roadmap em vez de simular evidência. Vários conselheiros convergiram que 'propor um arcabouço' e 'demonstrar um sistema' são papers diferentes sendo tratados como um só.

*Onde o conselho diverge:* submeter já à Automation in Construction × segurar por uma validação em FEM. O Cético vê desk-reject num journal aplicado; o Expansionista vê um framework fundacional que ganha por chegar primeiro. A divergência se resolve pela política editorial real do journal, não pela qualidade do texto.

*Pontos cegos pegos na revisão:* o Olhar Externo notou que boa parte da objeção do revisor desaparece se o enquadramento de 'framework conceitual' estiver explícito já na abertura, algo que a Discussão faz, mas que título e abstract precisam sinalizar com a mesma honestidade.

*Recomendação:* não decida por instinto. Primeiro caracterize o journal: amostre papers recentes da Automation in Construction e veja se framework/review sem validação tem espaço. Se tiver, submeta agora com a contribuição reposicionada em torno da escala L0–L5 e um enquadramento explícito de roadmap. Se não tiver, ou mire um journal mais receptivo a frameworks, ou adicione um estudo de caso só-FEM como evidência mínima.

*A primeira coisa a fazer:* hoje, levante cinco artigos recentes da Automation in Construction e marque cada um como empírico vs. conceitual. Esse levantamento decide entre 'submeter já' e 'segurar' antes de qualquer discussão de mérito.

---

## Integração com os outros skills

O conselho **decide**; os outros skills **executam** a decisão. Encaminhe conforme o veredito:

- Decisão de enquadramento, contribuição ou redação → `escritor-cientifico`, `pesquisador-senior`.
- Decisão sobre rigor metodológico, estatística ou guideline → `revisor-critico`, `estatistica-reporting`, `reporting-guidelines`, `revisao-sistematica-prisma`.
- Decisão sobre interpretação dos achados, "So What?" ou calibragem de limitações → `discussao-limitacoes`.
- Decisão sobre elementos visuais e deliverables (figuras, tabelas, highlights, graphical abstract) → `figuras-tabelas`, `highlights-graphical-abstract`.
- Decisão sobre journal, formatação, cover letter ou submissão → `editor-cientifico`.
- Decisão sobre como responder a revisores → `resposta-revisores`.
- Decisão de rodar o ciclo completo de produção do artigo → `workflow-artigo`.
- Quando a execução não cai em um skill específico → `cientista` (persona-default).
- Antes de entregar qualquer texto que o conselho recomende → `anti-vicios-ia` (limpeza de assinatura de IA).

---

## Notas importantes

- **Sempre dispare os 5 conselheiros em paralelo.** Disparo sequencial desperdiça tempo e deixa respostas anteriores vazarem para as seguintes.
- **Sempre anonimize para a revisão por pares.** Se os revisores souberem quem disse o quê, vão deferir a certos estilos em vez de avaliar pelo mérito.
- **O presidente pode discordar da maioria.** Se 4 de 5 dizem "faça", mas o raciocínio do dissidente é o mais forte, o presidente fica com o dissidente e explica por quê.
- **Não convoque o conselho para trivialidades.** Se a pergunta tem uma resposta certa, responda direto. O conselho é para incerteza genuína em que múltiplas perspectivas agregam.
- **A entrega é no chat, em markdown, nunca HTML nem arquivo.** A transcrição só é salva mediante pedido (Passo 6). A maioria dos usuários escaneia o veredito: mantenha-o limpo e escaneável.
