# Avaliação da Confiabilidade

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Confiabilidade** do i-Educar.

## 1. Introdução

[PREENCHER: Faça uma breve introdução sobre este objetivo.
* Qual era o objetivo (Goal) GQM definido na Fase 2 para Confiabilidade?
* Por que avaliar a confiabilidade deste software é importante (relembre o contexto da Fase 1, como as reclamações dos usuários)?
* Quais subcaracterísticas (Maturidade, Tolerância a Falhas, Recuperabilidade) foram investigadas?]

## 2. Referencial Teórico

[PREENCHER: Apresente a base teórica *para as métricas* que serão mostradas.
* **Maturidade:** Defina o que é a maturidade do software e por que métricas como "Densidade de Defeitos" e "Commits de Correção" são usadas para medi-la.
* **Tolerância a Falhas:** Defina o que é tolerância a falhas e como o "Índice de Tratamento de Exceções" se relaciona com este conceito.
* **Recuperabilidade:** Defina o que é recuperabilidade e por que uma "Análise Qualitativa de Backup" é crucial para ela.
* Lembre-se de citar as fontes (livros, artigos, normas ISO) que você usou na Fase 1 e 2.]

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Confiabilidade.

???+ "M1.1: Densidade de Defeitos no Código"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** API do GitHub (Issues) e `cloc`.
    * **Dados Coletados:**
        * Número total de issues com a label `bug`: [PREENCHER]
        * Total de linhas de código (KLOC) (PHP): [PREENCHER]
        * Cálculo: `([Issues] / [KLOC])` = [VALOR FINAL]

    ![Evidência da contagem de bugs]
    ![Evidência da contagem de linhas]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL] bugs/KLOC
    * **Critério (da Fase 2):**
        * Excelente: ≤ 1 bug/KLOC
        * Bom: >1 e ≤3 bugs/KLOC
        * Regular: >3 e ≤6 bugs/KLOC
        * Insatisfatório: >6 bugs/KLOC
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse número significa? Um valor X indica que o sistema tem muitos/poucos defeitos em relação ao seu tamanho. Isso valida/invalida a H1.1? Por quê? Qual o impacto disso para a estabilidade do código?]

??? "M1.2: Percentual de Commits de Correção"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `git log`
    * **Comandos executados:**
        * `git log --oneline --no-merges | wc -l` (Período: [Datas])
        * `git log --grep="fix|corrige|bugfix" --regexp-ignore-case --oneline --no-merges | wc -l` (Período: [Datas])
    * **Dados Coletados:**
        * Total de commits: [PREENCHER]
        * Commits de correção: [PREENCHER]
        * Cálculo: `([Correção] / [Total]) * 100` = [VALOR FINAL]%

    ![Evidência dos comandos git log]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Excelente: ≤ 10%
        * Bom: >10% e ≤20%
        * Regular: >20% e ≤35%
        * Insatisfatório: >35%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse percentual indica? Um valor alto sugere que a equipe gasta mais tempo corrigindo bugs (reativo) do que criando features (proativo). Isso valida/invalida a H1.2? Qual o impacto disso para a maturidade do projeto?]

??? "M2.1: Índice de Tratamento de Exceções"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** Revisão manual / Scripts de análise estática (`grep`/`ack`).
    * **Operações críticas definidas:** `new PDO(`, `pg_connect`, `fopen`, `file_put_contents`, etc.
    * **Dados Coletados:**
        * Número total de operações críticas: [PREENCHER]
        * Número de operações críticas *dentro* de um `try-catch`: [PREENCHER]
        * Cálculo: `([Com try-catch] / [Total]) * 100` = [VALOR FINAL]%

    ![Evidência da busca por operações críticas]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Excelente: ≥ 90%
        * Bom: 70%–89%
        * Regular: 40%–69%
        * Insatisfatório: < 40%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse índice revela sobre a robustez (tolerância a falhas) do sistema? Um valor baixo indica que falhas de I/O (ex: banco de dados offline) provavelmente causarão um crash no sistema. Isso valida/invalida a H2.1?]

??? "M3.1: Análise Qualitativa de Código de Backup"

    ### Evidências e Dados Brutos

    * **Método:** Inspeção manual do código (Localização: [PREENCHER CAMINHO DO ARQUIVO])
    * **Checklist de Análise (Pontuação 0-2):**
        * Documentação (Comentários): [0/1/2]
        * Clareza do Código (Nomes de variáveis): [0/1/2]
        * Tratamento de Erros: [0/1/2]
        * Configuração (Externalizada vs. Hard-coded): [0/1/2]
        * Testabilidade: [0/1/2]
    * **Cálculo (Soma):** [PONTUAÇÃO TOTAL] / 10

    ![Trecho do código de backup (Clareza)]
    ![Trecho do código de backup (Tratamento de Erros)]

    ### Classificação da Métrica

    * **Resultado:** [PONTUAÇÃO TOTAL] / 10
    * **Critério (da Fase 2):**
        * Excelente: 9–10
        * Bom: 7–8
        * Regular: 4–6
        * Insatisfatório: 0–3
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que essa pontuação qualitativa significa? O código de backup é fácil ou difícil de manter? Se a pontuação for baixa (validando H3.1), isso representa um risco alto para a recuperabilidade do sistema, pois os desenvolvedores podem ter dificuldade em corrigir ou adaptar essa rotina crítica.]

---

## 4. Conclusão (Confiabilidade)

[PREENCHER: Faça uma conclusão *específica* para a Confiabilidade.
* Com base nos resultados das 4 métricas, o objetivo de Confiabilidade foi atingido?
* Use os "Critérios para Julgamento" da Fase 2 (Aceitável, Parcialmente aceitável, Inaceitável) para dar um veredito sobre esta característica.
* Quais foram os principais pontos fortes e fracos encontrados?
* (Opcional) Quais hipóteses (H1.1, H1.2, H2.1, H3.1) foram validadas ou invalidadas pela coleta?]