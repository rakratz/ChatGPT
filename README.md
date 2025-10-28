# ChatGPT na Prática: criando GPTs personalizados + mapeamento de processos em BPMN

Aprenda, passo a passo, a **criar GPTs personalizados** e a **gerar/editar diagramas BPMN** (compatíveis com [bpmn.io](https://bpmn.io)) para acelerar descobertas, padronizar rotinas e documentar processos — com exemplos reais de manufatura (ex.: **OEE Coach**), serviços e backoffice.

## 🎯 Objetivos do curso

* Construir **GPTs personalizados** que gerem artefatos úteis (textos, planilhas, **arquivos `.bpmn`**).
* Mapear processos em **BPMN 2.0**, do *happy path* às exceções e gateways de decisão.
* Conectar os dois mundos: **do prompt ao diagrama** — produzindo um `.bpmn` que abre direto no **bpmn.io**.
* Disponibilizar **templates** e **prompts reutilizáveis** para sua equipe.

---

## 👥 Público-alvo

* Profissionais de **manufatura**, **qualidade**, **logística**, **TI** e **backoffice**.
* Times de **Process Excellence**, **PMO**, **Lean/Kaizen** e **Transformação Digital**.
* Docentes e estudantes que desejam **aprender na prática**.

---

## ✅ Pré-requisitos

* Noções básicas de fluxos de processo.
* Conta no **ChatGPT** (para criar/usar GPTs personalizados).
* Navegador moderno para abrir o **bpmn.io**.

---

## 📦 Estrutura do repositório

```
.
├─ /bpmn/
│  ├─ exemplos/
│  │  ├─ devolucao_cd.bpmn
│  │  ├─ oee_quickcheck.bpmn
│  │  └─ processo_generico_exemplo.bpmn
│  └─ templates/
│     ├─ template_processo_simples.bpmn
│     └─ template_swimlanes.bpmn
│
├─ /gpts/
│  ├─ OEE_Coach/
│  │  ├─ prompt_instrucoes.md
│  │  ├─ amostras_entrada_saida.md
│  │  └─ datasets_demo/
│  │     └─ producao_turno_exemplo.csv
│  └─ BPMN_Builder/
│     ├─ prompt_instrucoes.md
│     ├─ exemplos_de_uso.md
│     └─ snippets_bpmn.md
│
├─ /docs/
│  ├─ guia_bpmn_essencial.md
│  ├─ guia_gpts_personalizados.md
│  └─ caderno_de_exercicios.md
│
├─ .gitignore
└─ README.md
```

> Dica: mantenha seus **processos reais** em uma pasta separada (`/bpmn/projetos/`) para não misturar com os exemplos do curso.

---

## 🧪 Exemplos principais (o que você vai rodar)

### 1) **BPMN Builder (GPT personalizado)**

Um GPT que transforma uma **descrição de processo** em um **arquivo `.bpmn`** pronto para abrir no bpmn.io.

* **Entrada (prompt):** descrição do processo (papéis/lanes, atividades, decisões, exceções).
* **Saída:** XML BPMN válido (.bpmn).
* **Onde está:** `/gpts/BPMN_Builder/prompt_instrucoes.md` + `/gpts/BPMN_Builder/snippets_bpmn.md`.

**Como usar**

1. Abra o bpmn.io: [https://demo.bpmn.io](https://demo.bpmn.io)
2. Clique **Open Diagram** → selecione um `.bpmn` em `/bpmn/exemplos/` **ou** cole o XML gerado pelo GPT (**File → Import from Clipboard**).
3. Edite e salve.

> Exemplo pronto: `bpmn/exemplos/devolucao_cd.bpmn` (processo “Devolução no Centro de Distribuição”).

---

### 2) **OEE Coach (GPT personalizado)**

Um GPT focado em **Overall Equipment Effectiveness**: recebe dados, calcula **OEE = Disponibilidade × Performance × Qualidade**, interpreta e sugere **micro-plano de ataque** (perdas primárias).

* **Entrada:** Disponibilidade (%), Performance (%), Qualidade (%) e, opcionalmente, dados de turno/ativo.
* **Saída:** cálculo do OEE, *pareto* das perdas (texto), metas rápidas e plano de ação.
* **Onde está:** `/gpts/OEE_Coach/prompt_instrucoes.md` + dataset demo em `/gpts/OEE_Coach/datasets_demo/`.

**Exemplo rápido**

```
Disponibilidade=78%
Performance=85%
Qualidade=97%
```

**Cálculo:** `OEE = 0,78 × 0,85 × 0,97 ≈ 64,3%`
**Ataque prioritário:** atacar **Disponibilidade** (maior lacuna) com SMED, manutenção autônoma e controle de paradas.

---

## 🛠️ Como rodar os exemplos de BPMN

1. **Abrir um .bpmn existente**

   * Acesse [https://demo.bpmn.io](https://demo.bpmn.io)
   * **Open Diagram** → selecione, por ex., `bpmn/exemplos/devolucao_cd.bpmn`.

2. **Gerar um .bpmn via GPT**

   * Use o GPT “BPMN Builder”.
   * Cole sua especificação (veja *modelo de prompt* abaixo).
   * Baixe/salve o XML como `.bpmn` e **importe no bpmn.io**.

3. **Modelos de prompt — BPMN Builder**

```text
Quero um .bpmn (BPMN 2.0) válido para o bpmn.io.

Processo: Devolução no Centro de Distribuição
Papéis/Lanes: Transportador, Recebimento, Qualidade, Fiscal
Happy path (em ordem):
1) Transportador chega no CD e registra doca
2) Recebimento confere notas e agenda
3) Qualidade inspeciona integridade e validade
4) Recebimento registra retorno no WMS
Decisões:
- Notas ok? (se não: voltar para conferência)
- Aprovado na inspeção? (se não: segregar área de quarentena e abrir CAPA)
Exceções: falta de agendamento; divergência fiscal
Peça Start/End e inclua tempos como anotações.
```

> **IMPORTANTE:** o GPT deve **retornar somente o XML** BPMN entre blocos de código para facilitar o download.

---

## 🧩 Modelo de especificação de processo (checklist)

* **Propósito** e **gatilho** (Start Event).
* **Lanes/Papéis** (quem faz o quê).
* **Atividades** no *happy path* (ordem clara).
* **Gateways** de decisão (condições objetivas).
* **Exceções** e **tratamentos**.
* **Eventos de fim** (End Event) e saídas.
* **Anotações** (tempos, SLAs, riscos, sistemas: WMS/ERP/MES).

---

## 🧠 Criando seu GPT personalizado (guia relâmpago)

1. **Nome & Descrição**: claros e objetivos (ex.: *BPMN Builder* / *Gera arquivos .bpmn prontos para bpmn.io*).
2. **Instruções (System Prompt):**

   * Papel do GPT, **formato de saída** (ex.: *retorne apenas XML BPMN válido*).
   * Estilo de resposta (curto, direto, com validações mínimas).
   * Regras (ex.: manter sintaxe BPMN 2.0).
3. **Conhecimento (arquivos)**:

   * Suba **snippets** e **templates** (`/gpts/*/`).
4. **Testes de fumaça**:

   * Crie 3 prompts de teste rápidos.
   * Valide a importação no **bpmn.io**.
5. **Itere** com exemplos reais e guarde versões.

> Exemplos completos em: `/gpts/BPMN_Builder/` e `/gpts/OEE_Coach/`.

---

## 📚 Conteúdo do curso (visão geral)

1. **Fundamentos de GPTs personalizados**

   * System/Developer/User prompts • Boas práticas • *Guardrails* simples
2. **BPMN 2.0 essencial**

   * Eventos, Atividades, Gateways, Lanes • *Happy path* e exceções
3. **Do prompt ao diagrama**

   * Como emitir XML BPMN válido • Dicas para abrir no bpmn.io
4. **Estudos de caso**

   * **Devolução no CD** • **OEE Coach** • Processo genérico (serviços)
5. **Kit de produtividade**

   * Templates, checklists, reuso de prompts, versionamento no Git

---

## 🧾 Licença

Este repositório está licenciado sob **MIT**. Consulte `LICENSE`.

---

## 🤝 Contribuições

Contribuições são bem-vindas!
Abra uma **Issue** ou **Pull Request** com melhorias em:

* Modelos de prompt
* Templates BPMN
* Datasets e exemplos de manufatura/serviços

---

## 🧩 FAQ

**1. O arquivo `.bpmn` não abre no bpmn.io.**
Verifique se o GPT retornou **apenas** o XML BPMN entre blocos de código e se o arquivo foi salvo com **codificação UTF-8** e extensão `.bpmn`.

**2. O diagrama perde minhas Lanes/Pools.**
Confirme que o XML contém **`<bpmn:participant>`** (Pools) e **`<bpmn:lane>`** (Lanes). Use os **templates** em `/bpmn/templates/`.

**3. Como decidir onde atacar no OEE?**
Compare perdas: **Disponibilidade** (paradas), **Performance** (velocidade), **Qualidade** (refugos). Ataque primeiro a **maior lacuna**.

---

## 🔗 Atalhos úteis

* **Abrir BPMN online:** [https://demo.bpmn.io](https://demo.bpmn.io)
* **Pasta de exemplos:** `/bpmn/exemplos/`
* **Prompts principais:**

  * `/gpts/BPMN_Builder/prompt_instrucoes.md`
  * `/gpts/OEE_Coach/prompt_instrucoes.md`

---

## 📝 Créditos & Contato

Material didático preparado para o curso **“ChatGPT na Prática: GPTs personalizados + BPMN”**.
Sugestões, dúvidas e correções: abra uma *Issue* aqui no GitHub.

---

> **Bônus**: já deixei incluído o processo **“Devolução no Centro de Distribuição”** (`/bpmn/exemplos/devolucao_cd.bpmn`) com **Start/End**, **Lanes** (Transportador, Recebimento, Qualidade, Fiscal), **decisões**, **exceções** e **anotações de tempo**. Abra no bpmn.io e ajuste conforme sua realidade.
