# Revisão Crítica Consolidada (I-R-B-MB-E) — 2026-06-29

> Auditoria seção a seção por revisores independentes. As ações de severidade alta e média e a referência de conexão recomendada foram aplicadas após esta auditoria; os polimentos de severidade baixa também. Documento mantido como registro do processo.

---

# Revisão Crítica Consolidada
## *From Passive Members to Self-Aware Steel Structures* — submissão a *Automation in Construction*

Revisor-Crítico Chefe. Veredito calibrado à natureza **conceitual** do manuscrito (framework/review, sem experimentos). Tudo abaixo foi confrontado com as revisões seção a seção e com a verificação direta de dois artefatos críticos (`tab6-params.tex` e `highlights.txt`).

---

## 1. Quadro-síntese I-R-B-MB-E

| Seção | Nota | Justificativa em uma linha |
|---|:---:|---|
| Frontmatter (título/abstract/highlights/keywords) | **MB** | História central nítida e calibrada; pesa o highlight 4 ("detect") sobre-afirmativo e três lacunas triviais de calibragem no abstract. |
| 1. Introduction | **MB** | Fluxo O-QUE/POR-QUE/COMO resolvido e gap honesto; pesa densidade de equações modais redundantes e "understands" antropomórfico não operacionalizado. |
| 2. Background and related work | **MB** | Teoria densa e correta, equações verificadas, §2.6 de posicionamento forte; pesa mono-fonte (naser2023ml, brunton2019data) e dano→damping como lei geral. |
| 3. Paradigm + L0-L5 | **MB** | Distinção L0-L5 vs Rytter genuína e antropomorfismo pré-empacotado; pesa escopo L4-L5 não delimitado vs validação que alcança ~L3. |
| 4. Reference architecture | **MB** | Cinco camadas limpas, stance híbrido físico/ML rigoroso; **pesa regressão de confundidores para só-temperatura** e ausência de link camadas↔L0-L5. |
| 5. Methodology and testbed | **MB** | Linguagem "planned" exemplar e protocolo auditável; **pesa "pinned idealisation" residual na Tabela 6** (alta) e damping como fato empírico. |
| 6. ML strategy | **MB** | Pipeline bem fundado e ressalva de circularidade exemplar; pesa descasamento citação-conteúdo (SPRT/sohn2003) e nível do autoencoder inconsistente. |
| 7. Discussion | **MB** | Passa "So What?" com folga, circularidade e confundidores bem tratados; pesa arya2021roaddamage (pavimento) usado para "connection defects" em aço. |
| 8. Conclusions | **MB** | Recap disciplinado e calibragem "planned" explícita; **pesa arquitetura recapitulada como 4 camadas, omitindo a camada de decisão governada** (conflito com abstract). |
| **Coerência global** | **MB** | Passa teste dos 5 min, take-home consistente verbatim, 3 perguntas retomadas; só restam polimentos cosméticos no frontmatter. |
| **Referências** | **MB→E** | 24 refs, 10 AiC (mín. 5), zero DOIs quebrados, zero órfãs; só notas menores (venue fraco, lacuna de literatura de conexão). |

---

## 2. Comentários por seção (só o que importa)

### SEVERIDADE ALTA — corrigir antes de submeter

**A1. [Seção 5 / Tabela 6] A correção semirrígida não chegou ao artefato de especificação.**
`tabelas/tab6-params.tex` linha 11 ainda diz: `Connections & Bolt grade and preload; pinned idealisation; joint rotational stiffness`. Toda a prosa (Sec. 4, 5, 7, 8) foi migrada para "semi-rigid rotational spring", mas a **tabela que o paper apresenta como a especificação formal e auditável da campanha** continua dizendo "pinned idealisation". É exatamente onde um revisor checa coerência, e é uma contradição direta dentro da própria seção. **Verificado diretamente.**
*Ação:* editar para `Bolt grade and preload; semi-rigid joint rotational stiffness (bounded by pinned and rigid idealisations)`. "Pinned" só pode aparecer como caso-limite.

### SEVERIDADE MÉDIA — corrigir antes de submeter

**M1. [Seção 8] Recap da arquitetura como 4 camadas, omitindo a camada de decisão governada.**
A conclusão (l.5) lista sensing + FE baseline + digital twin + cognition (e ainda desdobra o digital-twin físico em dois itens), deixando de fora a *governed decision-and-reporting layer*. Isso conflita com o abstract ("five-layer architecture ... and a governed decision layer") e com a Sec. 4. Pior: a governança (baseline imutável versionado, gating humano, rollback) é uma das contribuições **mais distintivas** do paper e sustenta a alegação "autonomously reports" — omiti-la **subdimensiona a própria contribuição**.
*Ação:* reescrever a cláusula para espelhar as cinco camadas nomeadas e acrescentar uma cláusula no parágrafo de contribuição registrando que o reporte autônomo opera sob governança explícita.

**M2. [Seção 4] Regressão dos confundidores para só-temperatura (correção 2 não propagada).**
`04-architecture.tex` retorna zero ocorrências de "humidity", "wind" ou "operational load"; a camada de aquisição normaliza apenas temperatura. Como o abstract e as Seções 5/6/7 reivindicam um conjunto ampliado de confundidores, a arquitetura **fica aquém da própria correção**.
*Ação:* uma cláusula na camada de aquisição nomeando o conjunto ampliado e os canais que o capturam.

**M3. [Seção 6] Descasamento citação-conteúdo: SPRT vs Mahalanobis.**
O texto atribui "Mahalanobis distance, density- and isolation-based methods" a `sohn2003statistical`, que é especificamente sobre SPRT; a Tabela 5 lista a linha como "Outlier analysis / SPRT", mas o texto nunca menciona SPRT.
*Ação:* mencionar SPRT explicitamente como o detector sequencial de `sohn2003statistical`, deslocando Mahalanobis/density/isolation para a referência correta.

**M4. [Seções 6 e 7] arya2021roaddamage usado fora do escopo da fonte.**
`arya2021roaddamage` é detecção de dano em **pavimento rodoviário** por visão computacional, invocado em Sec. 7 (l.15) para "fatigue cracks and connection defects" em aço e em Sec. 6 (l.19) para ilustrar a "escala" do ramo supervisionado do testbed SHS/modal. É um salto de domínio que um revisor marca.
*Ação:* qualificar como domínio adjacente (escala de dataset apenas), ou reservar "connection defects" para `wangsu2023steelbearing`, mantendo arya2021 confinado ao parágrafo de visão como trabalho futuro.

**M5. [Seção 6] Nível do autoencoder inconsistente entre três lugares.**
Tabela 5 atribui ao autoencoder "L2-L3"; o texto da Sec. 6 e a Tabela 3 colocam toda a novelty detection unsupervised (existence/location) em **L3**. Confunde camada de feature (L2, onde vivem os latents) com camada de diagnóstico (L3, onde o erro de reconstrução decide).
*Ação:* padronizar o autoencoder como L3 (diagnóstico) na Tabela 5 e listar "autoencoder latents" separadamente em L2 na linha de feature extraction.

**M6. [Frontmatter] Highlight 4 com força acima da natureza conceitual** — ver Seção 5 deste relatório (força das afirmações).

**M7. [Seção 5] Damping no afrouxamento de parafuso afirmado como fato empírico** — ver Seção 5 deste relatório.

### SEVERIDADE BAIXA (agrupados — polimento)

- **[Intro]** Mover as equações modais (autoproblema repetido em l.5 e l.9) para o Background; na Introdução, prosa. Operacionalizar "cognition/understands" com uma cláusula ("operational, not phenomenological sense").
- **[Background]** Distribuir 1-2 citações primárias nas afirmações algorítmicas mono-fonte (LSTM/vanishing-gradient, SHAP/LIME); ancorar o elo autoencoder→anomalia em um trabalho de SHM aplicado; situar DMD/SINDy como repertório de fundo, não componentes do testbed.
- **[Sec. 3]** Adicionar frase delimitando quais níveis o testbed exercita (L1-L3 diretamente; L4-L5 só arquiteturalmente). Suavizar "understands" → "interprets" na l.28. Justificar por que L3 absorve quatro estágios de Rytter e L4 só um. Citar Rytter primário ao lado de farrar2013shm.
- **[Sec. 4]** Suavizar "make ... real-time" → alvo de projeto com latency budget; trocar "trustworthy" → "interpretable and auditable"; ligar a rigidez da mola às features que a identificam (observabilidade); cruzar-referenciar L0-L5.
- **[Sec. 5]** Padronizar notação do autovetor modal ({φ} vs {D}) entre Sec. 4 e 5; especificar o *desenho* dos níveis de dano (nº de níveis, % de redução de rigidez, fração do torque nominal) ainda que simbólicos.
- **[Sec. 6]** Ancorar a extensão "prognosis" como o 5º nível consagrado por Farrar/Worden sobre a hierarquia de 4 de Rytter.
- **[Sec. 7]** Quebrar o parágrafo de validação (l.5) em dois; reduzir a re-explicação de Rytter (l.13) a uma referência cruzada à Sec. 3.
- **[Sec. 8]** Cruzar-referenciar a "six-step methodology" (Sec. 5.6) para evitar o aparente descompasso 6-vs-5 com a lista de cinco itens de trabalho futuro; harmonizar o rótulo do LSTM (self-supervised vs temporal modelling) entre abstract/corpo/conclusão.

---

## 3. Auditoria de referências (síntese)

- **Total:** 24 refs. **AiC:** 10 (mínimo 5 — atendido com folga: chiachio2022, zou2026deep, li2025edge, mariniello2025, parisi2022, he2022, karaaslan2021, yu2024, wangsu2023, arya2021).
- **Quebradas/fabricadas:** nenhuma. Todos os 19 DOIs resolvem no Crossref e batem com título/journal/ano. Os 5 livros (Farrar-Worden, Brunton-Kutz, Chopra, Naser, Cook) legitimamente sem DOI. Zero órfãs (used = defined), consistente com build 0 undefined.
- **Distribuição temporal:** saudável e atual — ~2/3 do corpus é 2021+; clássicos (8) são âncoras fundacionais justificadas. Entradas 2026 (zou2026deep, karyofyllas2025) são ahead-of-print reais verificadas.
- **Qualidade:** venues majoritariamente Q1 (AiC, MSSP, SHM, Sensors).
- **Problemas (todos menores):** (a) `wangcha2022unsupervised` em *Engineering Reports* é o venue mais fraco — substituível por algo em MSSP/SHM se houver; (b) sobre-ancoragem em `farrar2013shm` (dezenas de \citep) pode soar como dependência de fonte única — diversificar afirmações genéricas de SHM; (c) **lacuna temática real:** bibliografia fina em literatura de conexão aparafusada/junta semirrígida, justamente o que a metodologia/limitações apoiam só via Farrar/Chopra genéricos — adicionar **uma** referência dedicada a comportamento de conexão/bolt-loosening fecharia isso (e reforçaria M4/A1/M7); (d) `figueiredo2010machine` tem ano real 2011 (bib correto; só o citekey diz 2010 — inócuo).

---

## 4. Teste das três perguntas (O QUE / POR QUE / COMO)

| Pergunta | Presença | Clareza | Retomada na conclusão |
|---|---|---|---|
| **O QUE** | Sim — Intro l.13 declara a tripla contribuição (paradigma, escala L0-L5, arquitetura+metodologia). | Alta. | Sim, verbatim — Concl. l.5 "The contribution is threefold". |
| **POR QUE** | Sim — gap em contraste com a literatura (l.13) + frase-síntese "they sense, but they do not understand" (l.7). | Alta; gap isolado como delta específico, sem straw man. | Sim — impacto (segurança/custo/confiabilidade) com verbos calibrados ("promises", "point toward"). |
| **COMO** | Sim — arquitetura de 5 camadas + metodologia de 6 passos + testbed SHS rotating-unbalance. | Alta na prosa; não exige subseção numerada (correto para Elsevier). | Sim — cinco "concrete next steps" sequenciados. |

As três estão respondidas na prosa e retomadas. **Ressalva:** o COMO é levemente sobre-prometido na Sec. 3 (escala até L5) frente à validação que chega a ~L3 — delimitar (baixa) fecha o laço.

---

## 5. Força das afirmações (claims acima da natureza conceitual)

1. **[ALTA] Highlight 4 — "Supervised and unsupervised AI detect stiffness loss and bolt loosening."** *(verificado)* O presente factual "detect" afirma capacidade demonstrada, que o corpo nega explicitamente ("no experiments have yet been performed"; "class separability under the model's own assumptions, not performance on the physical structure"). Highlights são indexados isoladamente — risco de citação fora de contexto. **Recalibrar:** "Architecture targets supervised/unsupervised detection of stiffness loss and bolt loosening" (≤85 car.). O highlight 5 ("enables autonomous predictive maintenance") tem a mesma tensão de registro, menor severidade.

2. **[MÉDIA] Sec. 5, l.7 — afrouxamento de parafuso "typically increases energy dissipation, producing ... a rise in vibrational damping."** Força de fato empírico num estudo sem dados; a magnitude e até o sinal do efeito de damping dependem do regime de preload (atrito de Coulomb não-linear, dependência de amplitude). É parte da **hipótese a testar**, não um dado. Recalibrar para "is expected to ... and may increase damping through frictional slip ... among the features the system is designed to test for." Mesma observação vale para Background l.9, Sec. 7 l.5 (baixa) e Fig. fig:frf.

3. **[MÉDIA] Sec. 4, l.15 — "make this comparison fast enough for real-time, streaming operation."** Capacidade computacional exigente apresentada como fato; suavizar para alvo de projeto sujeito a latency budget.

4. **[MÉDIA] Sec. 4, l.23 — "trustworthy through explainable-ML."** XAI entrega interpretabilidade/auditabilidade, não trustworthiness. Trocar.

5. **[BAIXA] "understands"** (Intro l.11; Sec. 3 l.28; Concl. l.3) — verbo mentalista forte para um mecanismo de comparação de resíduo. A Sec. 3 l.5 pré-empacota o disclaimer operacional, mas ele sai de vista downstream. Trocar por "interprets" onde o caveat não está adjacente, ou re-anexar a qualificação localmente.

6. **[BAIXA] Abstract — "advancing cognitive digital twins..."** gerúndio aceitável, no limite; "perceives... reports... through a permanent link to a continuously updated digital twin" em presente afirmativo é salvo por "proposes" na frase anterior, mas a única marca de status planejado é "specified". Trocar "specified" → "proposed" reforça.

Nenhum resultado numérico fabricado foi encontrado em nenhuma seção. As métricas (ROC, F1, balanced accuracy) são consistentemente apresentadas como o que **será** reportado.

---

## 6. Verificação das quatro correções recém-aplicadas

| # | Correção | Status | Detalhe |
|---|---|:---:|---|
| **(a)** | Conexões semirrígidas | **Coerente na prosa, mas com 1 falha residual ALTA** | Propagada verbatim em Sec. 4 (l.15), 5 (l.7/l.19), 7 (l.17, que até sinaliza a mudança), 8 (l.12), sem resíduo "pinned" no texto. **Porém** `tab6-params.tex` l.11 **ainda diz "pinned idealisation"** (verificado). A correção está 95% feita; falta o artefato de especificação. Corrigir é trivial e obrigatório. |
| **(b)** | Confundidores ambientais expandidos | **Coerente, com 1 regressão MÉDIA** | Bem feito em Sec. 6 (l.11) e Sec. 7 (l.11: "operational loads, wind and humidity ... separated statistically rather than measured away"). **Porém** Sec. 4 regrediu a só-temperatura (zero "humidity/wind/operational load") e Sec. 5 (l.23 + Tabela 4) só instrumenta temperatura. Abstract não menciona normalização (lacuna baixa). Alinhar Sec. 4/5 ao conjunto ampliado. |
| **(c)** | Ressalva de circularidade da validação sintética | **Bem integrada** | Exemplar em Sec. 7 l.5 e Sec. 6 l.27 ("specification of the validation protocol ... rather than evidence of field capability"), ecoada em Sec. 5 l.38 e Sec. 8 l.9. Único refinamento (baixa): repeti-la no ponto exato da Sec. 5 (instrumentação/integração) onde o leitor metodológico a procura, e no ponto da Sec. 4 l.19 (FEM como fonte de dados). Coerente. |
| **(d)** | Parágrafo CNN/visão como trabalho futuro | **Bem integrada, com 1 fricção MÉDIA** | Corretamente AUSENTE de abstract/highlights/conclusão; confinada a Sec. 7 l.15 ("Multimodal perception ... left to future work"), ancorada em karaaslan2021attention e arya2021roaddamage (ambas AiC reais). **Fricção:** arya2021roaddamage também aparece no corpo validável da Sec. 6 (l.19) e é usada para "connection defects" em aço fora do escopo da fonte (pavimento) — ver M4. Além disso karaaslan2021attention (segmentação semi-supervisionada) é sobrecarregada para ancorar "transfer learning" na Sec. 7 l.7. Realinhar fonte↔alegação fecha a correção. |

**Veredito da verificação:** as quatro correções estão conceitualmente integradas e propagadas para o frontmatter e a narrativa central sem contradição de história. Restam **três pontos materiais de fechamento**: o "pinned" da Tabela 6 (a, ALTA), a regressão de confundidores na arquitetura/metodologia (b, MÉDIA) e o realinhamento fonte↔alegação da CNN (d, MÉDIA).

---

## 7. Avaliação geral

### Nota final do manuscrito: **MB (Muito Bom)**

Manuscrito maduro, honesto quanto ao gênero conceitual e bem ancorado. Passa os quatro testes de coerência global (5 minutos, take-home, três perguntas, objetivos→metodologia→conclusões). A calibragem temporal das afirmações é, na quase totalidade, exemplar para um paper sem experimentos: nenhum resultado fabricado, ressalva de circularidade explícita, status "planned" reiterado. As referências satisfazem com folga a regra de ≥5 citações AiC e não têm entradas quebradas ou fabricadas.

**Não é E** por uma única inconsistência interna de alta severidade (Tabela 6) e um conjunto de fricções de média severidade — todas de correção mecânica, nenhuma estrutural ou de tese. Resolvidas as três ações prioritárias abaixo, o manuscrito sobe a **E** e está pronto para submissão.

### AS 3 AÇÕES PRIORITÁRIAS ANTES DE SUBMETER

1. **Eliminar o "pinned idealisation" residual da Tabela 6** (`tabelas/tab6-params.tex`, l.11) → "semi-rigid joint rotational stiffness (bounded by pinned and rigid)". É a única contradição interna de alta severidade; está no artefato de especificação que o revisor inspeciona para coerência. *(A1)*

2. **Restaurar a 5ª camada (decisão governada) no recap da conclusão** (Sec. 8, l.5) e propagar o conjunto ampliado de confundidores para a Seção 4 (e Tabela 4/Sec. 5). São os dois descasamentos abstract↔corpo de média severidade que um revisor cruza primeiro; ambos **subdimensionam** contribuições reais do paper. *(M1 + M2)*

3. **Recalibrar a força de duas afirmações-chave:** o highlight 4 ("detect" → "targets/designed to flag") e a frase de damping da Sec. 5 ("typically increases ... producing" → "is expected to ... may increase"). São os dois pontos onde a força excede a natureza conceitual declarada do paper — o highlight porque é indexado isoladamente, a frase de damping porque antecipa um resultado a medir. *(M6 + M7)*

> Recomendado também, no mesmo passe (baixo custo, alto retorno de robustez): realinhar arya2021roaddamage/karaaslan2021attention ao escopo das fontes (M4) e adicionar **uma** referência dedicada a conexão aparafusada/semirrígida (fecha a lacuna temática da bibliografia e reforça simultaneamente A1, M7 e M4).

Arquivos verificados nesta consolidação: `g:\ArtigoComDarlan2\artigo\tabelas\tab6-params.tex` (linha 11: "pinned idealisation" confirmado), `g:\ArtigoComDarlan2\artigo\highlights.txt` (linha 4: "detect" confirmado).
