# Avaliação da Manutenibilidade

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Manutenibilidade** do i-Educar.

## 1. Introdução

[PREENCHER: Faça uma breve introdução sobre este objetivo.
* Qual era o objetivo (Goal) GQM definido na Fase 2 para Manutenibilidade?
* Por que avaliar a manutenibilidade é vital para este projeto (software open-source, comunidade de desenvolvedores)?
* Quais questões principais (Impacto das Alterações, Complexidade de Entendimento, Cobertura de Testes) foram investigadas?]

## 2. Referencial Teórico

[PREENCHER: Apresente a base teórica *para as métricas* que serão mostradas.

* **Acoplamento (CBO):** Coupling Between Objects (CBO) é uma métrica de design da orientação a objetos [1] que mede o grau de interdependência de uma classe, ou seja, quantas outras classes uma classe específica utiliza. Essa medição é importante pois valores de CBO altos podem indicar diversos problemas, como o efeito cascata, onde uma alteração em uma classe pode atrapalhar o funcionamento de diversas outras classes que dependem dela.

* **Código Repetido:** Explique o "custo" do código duplicado (manutenção em N lugares).

* **Complexidade Ciclomática (CC):** Defina o que é CC (McCabe) e por que valores acima de 10 são considerados "Insatisfatórios" (dificuldade de teste e entendimento).

* **Cobertura de Teste e Densidade:** Explique o que é cobertura de linha e por que ela, sozinha, não é suficiente (daí a necessidade da "Densidade de Testes").

* **Tempo de Execução:** Por que testes lentos impactam o ciclo de desenvolvimento (CI/CD, feedback lento).

* Lembre-se de citar as fontes (livros como "Clean Code" de Robert C. Martin, artigos, etc.).]

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Manutenibilidade.

???+ "M1.1: Coupling Between Objects (CBO)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpmd` e SonarQube.
    * **Passo a Passo da Coleta:** 

        1. Executar a análise do `phpmd` no diretório /app, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd app/ xml codesize,design > phpmd_app.xml`

        2. Executar a análise do `phpmd` no diretório /src, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd src/ xml codesize,design > phpmd_src.xml`

        3. Filtrar o XML do /app para extrair apenas as violações de CBO (CouplingBetweenObjects): `grep 'rule="CouplingBetweenObjects"' phpmd_app.xml > cbo_app.txt`

        4. Filtrar o XML do /src para extrair apenas as violações de CBO: `grep 'rule="CouplingBetweenObjects"' phpmd_src.xml > cbo_src.txt`

        5. Consolidar manualmente os dados dos arquivos cbo_app.txt e cbo_src.txt em uma planilha Excel (Diretório, Classe, Valor CBO).

        6. Iniciar o serviço do SonarQube para a coleta da contagem total de classes: `sudo systemctl start sonarqube`

        7. Acessar a interface do SonarQube (http://localhost:9000) e coletar a contagem total de classes dos diretórios /app e /src.
    * **Dados Coletados:**
        * Valor médio de CBO: 18
        * Número/Percentual de classes com CBO ≥ 15: 1,70%
    * **Execução da Coleta**: [link para o vídeo com a execução da coleta]
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)

    ### Classificação da Métrica

    * **Resultado:** Média 18 | 1,70% das classes é "Insatisfatório"
    * **Critério (da Fase 2):**
        * Bom: CBO < 13
        * Regular: 13 ≤ CBO < 15
        * Insatisfatório: CBO ≥ 15
    * **Classificação:** Bom

    ### Análise e Discussão

    O nível de acoplamento geral do i-Educar não é ruim e nem um grande problema, a porcentagem de classes com CBO alto é uma porcentagem muito baixa comparado ao numero total de classes. Entretanto, as classes que possuem um CBO insatisfatório (14), possuem um valor de CBO excessivamente alto, como no caso da classe "AcademicYearService" que possui um CBO igual a 27, dificultando bastante uma futura alteração ou manutenção.

    Isso valida parcialmente a hipótese `(H1.1)` pois uma alteração em uma das 14 classes com CBO classificado como insatisfatório pode afetar diretamente no tempo de implantação de correções, pois, tomando "AcademicYearSearch" como exemplo novamente, pode ser necessário a correção em outras 27 classes em alguma correção.

??? "M1.2: Percentual de Código Repetido"

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

??? "M2.1: Complexidade Ciclomática (CC)"

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

??? "M3.1: Percentual de Cobertura de Teste (Line Coverage)"

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

??? "M3.2: Densidade de Testes (Testes/KLOC)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `grep` e `cloc`.
    * **Dados Coletados:**
        * Nº total de testes (`grep -r "function test" tests/ | wc -l`): [PREENCHER]
        * Linhas de código de produção totais (`cloc src/`): [PREENCHER]
        * Cálculo: `(Nº Total de Testes / (Linhas Totais de Código / 1000))` = [VALOR FINAL] Testes/KLOC

    ![Evidência da contagem de testes e linhas totais]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL] Testes/KLOC
    * **Critério (da Fase 2):**
        * Bom: > 10 Testes/KLOC
        * Regular: 5 a 10 Testes/KLOC
        * Insatisfatório: < 5 Testes/KLOC
    * **Classificação:** [PREENCHER: Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que essa densidade global mostra? Ela complementa a cobertura. Podemos ter alta cobertura (M3.1) mas baixa densidade, indicando testes grandes que cobrem muito código superficialmente. Como o resultado se compara com a H3.1?]

??? "M3.3: Tempo Médio de Execução dos Testes"

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

---

## Referências Bibliográficas

> [1] CHIDAMBER, Shyam R.; KEMERER, Chris F. A Metrics Suite for Object Oriented Design. IEEE Transactions on Software Engineering, v. 20, n. 6, p. 476-493, jun. 1994.

> [2] ...