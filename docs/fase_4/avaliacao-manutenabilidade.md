# Avaliação da Manutenibilidade

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Manutenibilidade** do i-Educar.

## 1. Introdução

[PREENCHER: Faça uma breve introdução sobre este objetivo.
* Qual era o objetivo (Goal) GQM definido na Fase 2 para Manutenibilidade?
* Por que avaliar a manutenibilidade é vital para este projeto (software open-source, comunidade de desenvolvedores)?
* Quais questões principais (Impacto das Alterações, Complexidade de Entendimento, Cobertura de Testes) foram investigadas?]

## 2. Referencial Teórico

[PREENCHER: Apresente a base teórica *para as métricas* que serão mostradas.
* **Acoplamento (CBO):** Defina o que é CBO (Coupling Between Objects) e por que valores altos são ruins (impacto em cascata).
* **Código Repetido:** Explique o "custo" do código duplicado (manutenção em N lugares).
* **Complexidade Ciclomática (CC):** Defina o que é CC (McCabe) e por que valores acima de 10 são considerados "Insatisfatórios" (dificuldade de teste e entendimento).
* **Cobertura de Teste e Densidade:** Explique o que é cobertura de linha e por que ela, sozinha, não é suficiente (daí a necessidade da "Densidade de Testes").
* **Tempo de Execução:** Por que testes lentos impactam o ciclo de desenvolvimento (CI/CD, feedback lento).
* Lembre-se de citar as fontes (livros como "Clean Code" de Robert C. Martin, artigos, etc.).]

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Manutenibilidade.

???+ "Métrica 1.1: Coupling Between Objects (CBO)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpmd` ou SonarQube.
    * **Comando:** `phpmd [caminho] xml codesize,coupling`
    * **Dados Coletados:**
        * Valor médio de CBO: [PREENCHER]
        * Número/Percentual de classes com CBO > 15: [PREENCHER]

    ![Saída da ferramenta de análise de CBO]

    ### Classificação da Métrica

    * **Resultado:** Média [X] / [Y]% das classes é "Insatisfatório"
    * **Critério (da Fase 2):**
        * Bom: CBO ≤ 10
        * Regular: 10 < CBO ≤ 15
        * Insatisfatório: CBO > 15
    * **Classificação:** [PREENCHER: Aderente a qual classificação? Focar nas classes "Insatisfatórias"]

    ### Análise e Discussão

    [PREENCHER: O que o nível de acoplamento indica? Um CBO alto sugere que as classes estão muito interligadas, tornando difícil alterar uma parte do sistema sem quebrar outra (efeito cascata). Isso valida H1.1? Qual o impacto no esforço de manutenção?]

??? "Métrica 1.2: Percentual de Código Repetido"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpcpd` (PHP Copy/Paste Detector) ou SonarQube.
    * **Comando:** `phpcpd [caminho]`
    * **Dados Coletados:**
        * Percentual de linhas duplicadas: [VALOR FINAL]%

    ![Saída da ferramenta de detecção de duplicação]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Bom: ≤ 3%
        * Regular: 3% < M1.2 ≤ 5%
        * Insatisfatório: > 5%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse valor significa? Código duplicado é um grande indicador de débito técnico. Se um bug for encontrado em um trecho copiado, ele precisará ser corrigido em N lugares. Isso valida H1.1 (junto com o CBO)? Qual o impacto no custo de manutenção?]

??? "Métrica 2.1: Complexidade Ciclomática (CC)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpmd` ou SonarQube.
    * **Comando:** `phpmd [caminho] xml codesize`
    * **Dados Coletados:**
        * Complexidade Ciclomática média por método: [PREENCHER]
        * Número/Percentual de métodos com CC > 10: [PREENCHER]

    ![Saída da ferramenta de análise de Complexidade]

    ### Classificação da Métrica

    * **Resultado:** Média [X] / [Y]% dos métodos é "Insatisfatório"
    * **Critério (da Fase 2):**
        * Bom: CC ≤ 5
        * Regular: 5 < CC ≤ 10
        * Insatisfatório: CC > 10
    * **Classificação:** [PREENCHER: Focar na quantidade de métodos "Insatisfatórios"]

    ### Análise e Discussão

    [PREENCHER: O que esses dados indicam? Métodos com alta CC (muitos `if`, `else`, `for`, `while`) são difíceis de entender, testar e modificar. Isso valida a H2.1? Qual o impacto no tempo de onboarding de novos desenvolvedores?]

??? "Métrica 3.1: Percentual de Cobertura de Teste (Line Coverage)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** PHPUnit com Xdebug/PCOV.
    * **Comando:** `phpunit --coverage-html [diretório]`
    * **Dados Coletados:**
        * Cobertura total de linhas (Line Coverage): [VALOR FINAL]%

    ![Relatório de Cobertura de Teste]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Bom: ≥ 80%
        * Regular: 70% ≤ M3.1 < 80%
        * Insatisfatório: < 70%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse percentual de cobertura significa? Ele mede a "confiança" que a equipe pode ter ao fazer refatorações. Um valor baixo (validando H3.1) indica um alto risco de introduzir regressões (quebrar algo que funcionava) a cada nova alteração.]

??? "Métrica 3.2: Densidade de Testes por Módulo (Testes/KLOC)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `grep` e `cloc`.
    * **Dados Coletados (Exemplo Módulo Escola):**
        * Nº de testes (Módulo Escola): [PREENCHER]
        * KLOC (Módulo Escola): [PREENCHER]
        * Cálculo (Escola): [VALOR FINAL] Testes/KLOC
    * **Dados Coletados (Exemplo Módulo Servidores):**
        * Nº de testes (Módulo Servidores): [PREENCHER]
        * KLOC (Módulo Servidores): [PREENCHER]
        * Cálculo (Servidores): [VALOR FINAL] Testes/KLOC
    * **Dados Coletados (Exemplo Módulo Educacenso):**
        * Nº de testes (Módulo Educacenso): [PREENCHER]
        * KLOC (Módulo Educacenso): [PREENCHER]
        * Cálculo (Educacenso): [VALOR FINAL] Testes/KLOC

    ![Evidência da contagem de testes e linhas por módulo]

    ### Classificação da Métrica

    * **Resultado:** (Escola: [X], Servidores: [Y], Educacenso: [Z])
    * **Critério (da Fase 2):**
        * Bom: > 10 Testes/KLOC
        * Regular: 5 a 10 Testes/KLOC
        * Insatisfatório: < 5 Testes/KLOC
    * **Classificação:** [PREENCHER: Classificar cada módulo]

    ### Análise e Discussão

    [PREENCHER: O que essa densidade mostra? Ela complementa a cobertura. Podemos ter alta cobertura (M3.1) mas baixa densidade, indicando testes grandes que cobrem muito código superficialmente. Ou podemos ter baixa cobertura mas alta densidade em um módulo específico, mostrando um foco de teste. Como esses módulos se comparam?]

??? "Métrica 3.3: Tempo Médio de Execução dos Testes"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** PHPUnit / Log do GitHub Actions.
    * **Dados Coletados:**
        * Tempo total de execução da suíte: [PREENCHER: ex: 5m 30s]
        * Número total de testes: [PREENCHER]
        * Cálculo (Tempo por teste): `([Tempo Total] / [Nº Testes])` = [VALOR FINAL]s por teste

    ![Evidência do tempo de execução dos testes]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]s (Tempo médio por teste)
    * **Critério (da Fase 2):**
        * Bom: ≤ 1s
        * Regular: 1s < M3.3 ≤ 3s
        * Insatisfatório: > 3s
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: Qual o impacto do tempo de execução? Se a suíte inteira demorar muito (ex: > 10 min) ou o tempo médio for alto (indicando testes lentos, talvez de integração disfarçados de unitários), os desenvolvedores param de rodá-la localmente. Isso valida H3.2? Se sim, o feedback de erros é atrasado até o pipeline de CI, tornando o desenvolvimento mais lento.]

---

## 4. Conclusão (Manutenibilidade)

[PREENCHER: Faça uma conclusão *específica* para a Manutenibilidade.
* Com base nos resultados das 6 métricas, o objetivo de Manutenibilidade foi atingido?
* Use os "Critérios para Julgamento" da Fase 2 (Aceitável, Parcialmente aceitável, Inaceitável) para dar um veredito sobre esta característica.
* Quais foram os principais pontos fortes e fracos encontrados? (Ex: "A cobertura de teste é boa, mas a complexidade e o acoplamento são 'Insatisfatórios', indicando um código difícil de manter.")
* (Opcional) Quais hipóteses (H1.1, H2.1, H3.1, H3.2) foram validadas ou invalidadas pela coleta?]