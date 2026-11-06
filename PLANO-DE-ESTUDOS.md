# Plano de Estudos — CCDV-F (Claude Certified Developer – Foundations)

## Contexto

O repositório é o livro *Claude Certified Developer – Foundations*: 23 capítulos que cobrem as 25 skills dos 8 domínios da prova. Você quer um plano detalhado para os **4 meses** até a prova.

- **Período:** seg 09/nov/2026 → semana de 01/mar/2027 (17 semanas)
- **Prova:** 53 itens em 120 min (múltipla escolha e múltipla resposta), escala de 100 a 1.000, **aprovação com 720**
- **Carga estimada:** ~7 h/semana (3 sessões de 1 h nos dias úteis + 3–4 h no fim de semana). Nas semanas de festas e de Carnaval a carga cai pela metade.

### O que o livro diz sobre a prova (e por que isso define o plano)
1. **Quase toda resposta errada é um mecanismo que funciona em outro contexto**: um Skill onde precisava de um servidor MCP, um arquivo de contexto onde precisava de um hook, um retry onde a falha era permanente. Decorar features não basta. É preciso saber **para que** cada mecanismo serve e onde fica a fronteira entre dois deles.
2. **Um terço da prova não é sobre Claude.** O Domínio 2 vale 33,1% e cobre REST, versionamento, revisão de código e fronteiras de aplicação. O Domínio 4 vale 2,6%. O tempo de estudo segue o peso de cada tema, não o interesse que ele desperta.
3. **O livro não tem questões de prática.** Por isso o plano inclui produzir questões próprias e usar fontes oficiais.

### Pesos por domínio ([95-coverage-map.md](book/chapters/95-coverage-map.md))
| Domínio | Peso | Capítulos |
|---|---|---|
| 2 Applications & Integration | **33,1%** | 3, 15, 16, 17, 18, 23 |
| 5 Model Selection & Optimization | **16,8%** | 1, 2, 4, 8 |
| 1 Agents & Workflows | **14,7%** | 12, 13 |
| 6 Prompt & Context Engineering | **11,0%** | 5, 6, 7 |
| 8 Tools & MCPs | **10,6%** | 9, 10, 11 |
| 7 Security & Safety | **8,1%** | 20, 21, 22 |
| 3 Claude Code | 3,1% | 14 |
| 4 Eval, Testing & Debugging | 2,6% | 19 |

Capítulos com mais peso: **12 (9,4%)**, **16 (8,6%)**, **17 (7,4%)**, **3 (6,8%)**, **2 (6,1%)**, **13 (5,3%)**, **1 (5,2%)**.

---

## Método: o ciclo de cada capítulo

Todo capítulo segue a mesma estrutura: resumo em itálico, seções cujos títulos já são a conclusão, anti-padrões em **negrito**, a seção "How Wrong Answers Are Built" e a lista "What to Remember". Cada capítulo passa por 5 passos:

1. **Pré-leitura (10 min):** leia o resumo, a lista de títulos `##` e o "What to Remember". Escreva o que você acha que cada título quer dizer.
2. **Leitura ativa (60–90 min):** leia o capítulo inteiro e liste num caderno **todos os termos em negrito** que nomeiam um erro, por exemplo *capacity-versus-selection confusion*.
3. **Flashcards (30 min):** transforme a tabela final de 3 colunas (*sinal no cenário → resposta usual → armadilha usual*) em cards no Anki ou similar: frente = sinal, verso = resposta + armadilha. Acrescente 1 card por linha do "What to Remember".
4. **Fonte primária (30 min):** abra 2–3 endnotes do capítulo na documentação oficial (platform.claude.com, docs do Claude Code, spec do MCP). O livro foi escrito até set/2026 e **números mudam**: confira valores, nomes de modelos e limites.
5. **Prática (30–90 min):** faça o lab da semana e escreva **3 questões de cenário próprias** no estilo da prova, com 4 opções em que todas são mecanismos reais e só uma é a certa.

**Revisão espaçada contínua:** 15 min de flashcards por dia, sempre. Aos sábados, releia os "What to Remember" de todos os capítulos já estudados.

**Teste de autoavaliação:** para cada linha do "What to Remember", você consegue justificá-la **com o livro fechado**? Marque 🟢 se consegue, 🟡 se hesita e 🔴 se não consegue. Os 🔴 voltam para a próxima semana de revisão.

---

## Cronograma semana a semana

### Fase 0: Diagnóstico e base (Semana 1)
**S1 · 09–15/nov — Cap. 0 (Prefácio) + Cap. 1 · 5,2%**
- Leia o prefácio, o [coverage map](book/chapters/95-coverage-map.md) e o [glossário](book/chapters/96-glossary.md) de forma rápida.
- **Diagnóstico:** leia os 23 "What to Remember" de uma vez e marque 🟢/🟡/🔴. O resultado mostra onde você começa.
- Cap. 1: tokens, janela de contexto como capacidade × temperatura como seleção, model × thinking × effort × fast mode, zero/one/multi-shot.
- **Setup:** crie a chave de API (Console Anthropic), instale o SDK Python ou TS e o Claude Code, e monte o baralho no Anki.
- Lab: envie a mesma requisição 5× com temperature 0 e compare as respostas. Meça tokens com o endpoint de token counting.

### Fase 1: Primeira passada profunda (Semanas 2–15)

**Parte II: a chamada e o modelo**
- **S2 · 16–22/nov — Cap. 2 · 6,1%** (as 4 partes de uma chamada, as 3 "costuras" onde ela falha, retries com padrão de 2 tentativas, os 11 códigos de erro e a costura de cada um, WebSocket × persistência)
  - Lab: provoque 400, 401, 429 e 529 (ou simule) e classifique qual merece retry. Monte uma tabela "código → costura → retry?" e memorize.
- **S3 · 23–29/nov — Cap. 3 · 6,8%** (Messages API, `stop_reason`, pareamento de tool_result por ID, streaming, imagens e documentos, Batches com 50% de desconto, provedores terceiros como Bedrock e Vertex)
  - Lab: a mesma tarefa via Messages, via streaming e via Batch. Trate cada `stop_reason` (`end_turn`, `max_tokens`, `tool_use`, `stop_sequence`...).
  - Regra central: **quem está esperando a resposta decide o formato da requisição**.
- **S4 · 30/nov–06/dez — Cap. 4 · 2,7% + Cap. 5 · 4,6%** (escolha de modelo por custo por tarefa concluída e pelo "décimo mais difícil", IDs de modelo congelados; posicionamento de instruções como decisão de confiança, delimitadores, exemplos, iteração baseada em evidência)
  - Lab: rode a mesma tarefa em Haiku, Sonnet e Opus e calcule o custo por tarefa concluída. Compare a mesma instrução no system prompt e no turno do usuário.

**Parte III: obter uma resposta utilizável**
- **S5 · 07–13/dez — Cap. 6 · 2,6% + Cap. 7 · 3,8%** (structured outputs, as 3 formas documentadas de um schema garantido falhar, validação ao receber, verificação com fonte externa ao modelo; contexto como orçamento, bloat × drift, compaction, isolamento com subagentes)
  - Lab: structured output com validação Pydantic/Zod e um destino definido para as falhas.
- **S6 · 14–20/dez — Cap. 8 · 2,8% + Revisão do Bloco A**
  - Cap. 8: os 4 preços (input, output, cache write, cache read), projeção de custo com 5 grandezas, atribuição de custo, prompt caching.
  - Lab: ative o prompt caching num prefixo grande e leia `cache_creation_input_tokens` e `cache_read_input_tokens`. Depois ligue o thinking e confirme que o cache é invalidado.
  - **Revisão:** os Domínios 5 e 6 ficam completos (caps 1, 2, 4, 5, 6, 7, 8). Reveja os 🔴 e escreva 10 questões de cenário misturando capítulos.

**Parte IV: ferramentas (semanas de festas, carga reduzida)**
- **S7 · 21–27/dez — Cap. 9 · 4,4%** (a descrição da tool é input do modelo e não documentação, o array `required`, validação no dispatch, erros acionáveis, sobreposição de tools)
  - Lab: duas tools com descrições ambíguas. Observe a escolha errada e depois corrija só a descrição.
- **S8 · 28/dez–03/jan — Cap. 10 · 2,1% + Cap. 11 · 4,1%** (MCP: tools, resources e prompts conforme quem decide usar cada um; transporte stdio × HTTP conforme onde o servidor roda; escopo de configuração; built-in × função custom × Skill × MCP, escolhido primeiro pela pergunta de onde o código precisa executar)
  - Lab: um servidor MCP mínimo em stdio conectado ao Claude Code. Um Skill simples (`SKILL.md`).

**Parte V: agentes**
- **S9 · 04–10/jan — Cap. 12 · 9,4% ⭐** (workflow × agente, as 5 formas de workflow, o coordenador e seus handoffs, o custo de ~15× os tokens de um chat, subagente que começa vazio, memória, frameworks)
  - Semana inteira para este capítulo, o de maior peso do livro. Desenhe à mão as 5 formas (prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer) e associe cada uma à condição que a seleciona.
  - Leitura extra: *Building Effective AI Agents* e *How we built our multi-agent research system* (links no README).
- **S10 · 11–17/jan — Cap. 13 · 5,3% + Cap. 14 · 3,1%** (Agent SDK, o loop de 5 passos, sessão = subprocesso, quando um loop próprio se justifica, residência de dados, hooks; modos de permissão do Claude Code, plan mode, escopos de settings, CLAUDE.md em camadas, os 5 componentes, execução headless com output forçado)
  - Lab: um agente com o Agent SDK. No Claude Code, configure um hook `PreToolUse` que bloqueia um comando e compare com a mesma regra escrita no CLAUDE.md.

**Parte VI: a aplicação em volta do modelo (Domínio 2, o mais pesado)**
- **S11 · 18–24/jan — Cap. 15 · 3,4% + Cap. 16 · 8,6% ⭐** (requisitos implícitos, residência de dados que elimina opções, registro de decisões; fronteiras da aplicação, instruções em cada interface, gate determinístico, fronteiras de conteúdo de entrada e de saída, schema como contrato entre 3 partes, continue/resume/fork, pinagem de plugins)
  - Dedique ~60% da semana ao Cap. 16.
- **S12 · 25–31/jan — Cap. 17 · 7,4% ⭐ + Cap. 18 · 4,1%** (contratos REST, concorrência, controle de versão, estágios de pipeline, revisor automatizado × merge gate, refatoração; model ID × alias, versionamento de prompt, superfícies de configuração, ambientes)
  - Este conteúdo é engenharia geral. Mesmo que você já domine, faça as questões, porque a prova cobra a interpretação do livro.

**Parte VII: o que dá errado**
- **S13 · 01–07/fev — Cap. 19 · 2,6% + Cap. 20 · 3,2%** (suíte verde × produto quebrado, classificação de erros, traces, médias; prompt injection × jailbreak, controles dentro ou fora do canal do atacante, autorização por operação)
- **S14 · 08–14/fev (Carnaval, leve) — Cap. 21 · 3,3% + Cap. 22 · 1,6%** (regra no prompt não é enforcement, camadas independentes, identidade como limite, hooks no tempo; segredos, rotação, expiração, verificação de identidade)

**Parte VIII: depois do deploy**
- **S15 · 15–21/fev — Cap. 23 · 2,8% + 1ª revisão geral**
  - Cap. 23: gates que conseguem recusar, a fase contínua após o go-live, deprecação de modelos.
  - Releia os 23 "What to Remember" e refaça o diagnóstico da S1. Compare os resultados.

### Fase 2: Revisão por peso e simulados (Semanas 16–17)

**S16 · 22–28/fev — Revisão dirigida + Simulado 1**
- Revise na ordem de peso: **D2** (caps 3, 16, 17, 15, 18, 23) → **D5** (1, 2, 4, 8) → **D1** (12, 13) → **D6** → **D8** → **D7** → D3 → D4.
- Releia só as seções "How Wrong Answers Are Built" e as tabelas de 3 colunas.
- **Simulado 1 (sábado):** 53 questões em 120 min, cronometrado (~2 min e 15 s por questão). Use o banco que você escreveu ao longo dos meses (~60+ questões) e complete com questões geradas por um LLM a partir das tabelas do livro. Peça cenários em que todas as opções são mecanismos reais.
- Analise os erros: para cada um, identifique qual **anti-padrão em negrito** você não reconheceu.

**S17 · 01–06/mar — Simulado 2, ajuste fino e prova**
- Seg/ter: Simulado 2 e revisão dos erros.
- Qua/qui: só flashcards e "What to Remember". Nada de conteúdo novo.
- Véspera: descanso e leitura leve dos 23 "What to Remember".
- **Na prova:** cada item diz quantas respostas marcar. Pergunte sempre **"sobre qual mecanismo esta opção age, e foi esse o mecanismo que o cenário mencionou?"** (heurística do Cap. 1).

---

## Recursos complementares
- **Exam guide oficial da Anthropic:** blueprint, pesos e eventuais questões de exemplo. É a fonte que manda sobre o livro.
- **Documentação oficial:** platform.claude.com/docs, docs do Claude Code, spec do MCP. Use os links das endnotes.
- **Anthropic Academy:** cursos gratuitos de API, MCP e Claude Code (confira o que está disponível no momento).
- **Os 7 posts de engenharia** listados no [README.md](README.md), sobretudo os de agentes (Cap. 12) e de evals (Cap. 19).
- **Guias do mesmo autor** para CCAR-F e CCAR-P (no README), como material extra de cenários.

## Metas de controle
| Marco | Data | Critério |
|---|---|---|
| Bloco A (D5 + D6) concluído | 20/dez | ≥ 80% 🟢 nos caps 1–8 |
| Partes IV–V concluídas | 17/jan | Labs de MCP, Skill, Agent SDK e hook executados |
| Leitura completa | 21/fev | 23 capítulos lidos, ~70+ questões próprias escritas |
| Simulado 1 | 27/fev | ≥ 75% de acertos (margem acima da nota de corte) |
| Simulado 2 | 02/mar | ≥ 80%, nenhum domínio abaixo de 65% |

## Verificação
- Toda semana: os flashcards da semana existem, o lab foi executado e as 3 questões foram escritas.
- Diagnóstico refeito na S15, com comparação explícita com o da S1.
- Os simulados têm resultado registrado por domínio. Se um domínio de peso alto (D2, D5, D1) ficar abaixo de 70%, a S17 é redistribuída para ele.
