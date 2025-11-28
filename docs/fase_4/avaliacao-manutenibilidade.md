# Avaliação da Manutenibilidade

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Manutenibilidade** do i-Educar.

## 1. Introdução

O objetivo definido para essa avaliação foi analisar o i-Educar com o foco na Manutenibilidade do ponto de vista da equipe de desenvolvimento utilizando o GQM na definição das questões, hipóteses e métricas.

A avaliação da manutenibilidade é vital para o i-Educar devido à sua natureza de software livre. Como um projeto open-source, a sustentabilidade do sistema depende da capacidade da comunidade de compreender, corrigir e evoluir o código de forma autônoma e a arquitetura do sistema, que combina código legado com implementações modernas, exige monitoramento constante da qualidade interna para evitar que o esforço técnico inviabilize futuras manutenções.

Tendo isso em vista, a investigação foi guiada por três questões fundamentais definidas na [fase 2](../fase_2/gqm_manutenibilidade.md) do processo de avaliação de qualidade de software.

1. **Impacto das alterações (Q1):** Avalia o risco de propagação de erros ao modificar o sistema, investigando acoplamento entre classes e duplicação de código.
2. **Complexidade de entendimento (Q2):** Mensura o quão difícil é para um desenvolvedor compreender a lógica interna dos métodos, utilizando a complexidade ciclomática.
3. **Situação dos testes (Q3):** Verifica a existência eficácia de uma rede de segurança automatizada (testes unitários e de integração).

## 2. Referencial Teórico

* **Acoplamento (CBO):** Coupling Between Objects (CBO) é uma métrica de design da orientação a objetos [1] que mede o grau de interdependência de uma classe, ou seja, quantas outras classes uma classe específica utiliza. Essa medição é importante pois valores de CBO altos podem indicar diversos problemas, como o efeito cascata, onde uma alteração em uma classe pode atrapalhar o funcionamento de diversas outras classes que dependem dela.

* **Código Repetido:** A duplicação de código representa trabalho, risco e complexidade extra, ela pode ser apresentada de várias formas, como linhas de código idênticas ou semelhantes e duplicação de implementação [3]. É importante a medição de código repetido, pois a duplicação aumenta o acúmulo de código, exige mais trabalho para manutenção e aumenta as chances de erros serem introduzidos ou omitidos.

* **Complexidade Ciclomática (CC):** A complexidade ciclomática segundo McCabe [4] é uma medida de complexidade baseada na teoria dos grafos. Ela serve para medir e controlar o número de caminhos em um programa e permite identificar módulos de software que serão difíceis de testar e manter. A medição da complexidade ciclomática de um código é importante, pois códigos com alta complexidade tendem a ter um número excessivo de caminhos de controle, tornando-o extremamente difícil de testá-lo e mantê-lo.

* **Cobertura de Teste e Densidade:** A cobertura de teste de linha (Line Coverage) é uma métrica quantitativa que indica o percentual de linhas de código executadas durante a execução de uma suíte de testes. Embora seja uma medida valiosa para identificar código não testado, ela, por si só, não é suficiente para garantir a qualidade dos testes [5]. Uma alta cobertura pode mascarar a existência de testes superficiais que executam o código mas não verificam adequadamente seu comportamento. Por isso, a Densidade de Testes (Testes/KLOC - número de testes por mil linhas de código) é uma métrica complementar importante, pois mede o esforço de teste em relação ao tamanho do código, ajudando a identificar se há um número adequado de casos de teste por unidade de código e fornecendo insights sobre a distribuição dos testes ao longo da base de código [6].

* **Tempo de Execução:** O tempo de execução dos testes é um fator crítico que impacta diretamente a produtividade da equipe de desenvolvimento e a eficiência do ciclo de desenvolvimento contínuo (CI/CD). Testes lentos criam um ciclo de feedback mais longo, desestimulando os desenvolvedores a executá-los com frequência e retardando a detecção de defeitos [7]. Em pipelines de integração contínua, suítes de teste demoradas aumentam o tempo de entrega, causam filas de builds e atrasam o deploy de correções críticas. A indústria recomenda que testes unitários sejam executados em menos de 1 segundo cada, permitindo ciclos rápidos de desenvolvimento e feedback imediato [8].

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Manutenibilidade.

???+ "M1.1: Coupling Between Objects (CBO)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpmd` e SonarQube.
    * **Passo a Passo da Coleta:** 

        1. Executar a análise do `phpmd` no diretório `/app`, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd app/ xml codesize,design > phpmd_app.xml`

        2. Executar a análise do `phpmd` no diretório `/src`, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd src/ xml codesize,design > phpmd_src.xml`

        3. Filtrar o XML do `/app` para extrair apenas as violações de CBO: `grep 'rule="CouplingBetweenObjects"' phpmd_app.xml > cbo_app.txt`

        4. Filtrar o XML do `/src` para extrair apenas as violações de CBO: `grep 'rule="CouplingBetweenObjects"' phpmd_src.xml > cbo_src.txt`

        5. Consolidar manualmente os dados dos arquivos `cbo_app.txt` e `cbo_src.txt` em uma planilha Excel (Diretório, Classe, Valor CBO).

        6. Iniciar o serviço do SonarQube para a coleta da contagem total de classes: `sudo systemctl start sonarqube`

        7. Acessar a interface do SonarQube (`http://localhost:9000`) e coletar a contagem total de classes dos diretórios `/app` e `/src`.

    * **Dados Coletados:**
        * Nº Total de Classes em `/app` e `/src`: 824
        * Nº de Classes captadas pelo `phpmd`: 22
        * Nº de Classes classificadas como "Insatisfatório": 14
        * Valor médio de CBO: 18
        * Número/Percentual de classes com CBO ≥ 15: `(14/824)*100 = 1,70%`
    * **Execução da Coleta**: Link para o vídeo da execução da coleta [Manutenibilidade - Métrica 1.1: Coupling Between Objects (CBO)](https://youtu.be/BjQ9_M7l6DQ)
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

    * **Ferramenta(s):** SonarQube.
    * **Dados Coletados:**
        * Densidade: 7,4%
        * Linhas Duplicadas: 25796
        * Blocos Duplicados: 2485
        * Arquivos Duplicados: 378
    * **Execução da Coleta**: Link para o vídeo da execução da coleta [Manutenibilidade - Métrica 1.2: Percentual de Código Repetido](https://youtu.be/CkMkUP5ixHU)
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)

    ### Classificação da Métrica

    * **Resultado:** 7,4%
    * **Critério (da Fase 2):**
        * Bom: ≤ 3%
        * Regular: 3% < M1.2 ≤ 5%
        * Insatisfatório: > 5%
    * **Classificação:** Insatisfatório

    ### Análise e Discussão

    De acordo com a análise pelo SonarQube, a densidade de código duplicado em todo o repositório do i-Educar é consideravelmente alta levando em consideração os critérios de julgamento definidos pela equipe. 

    Assim como o alto acoplamento, a duplicação de código está diretamente ligada aos problemas de manutenção de código (`H1.1`). De acordo com os dados obtidos pelo SonarQube, 2485 blocos de código são duplicados no código do i-Educar e, caso algum desses blocos precisem passar por algum tipo de correção, o retrabalho de manutenção nesse bloco será muito grande.

??? "M2.1: Complexidade Ciclomática (CC)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `phpmd` e SonarQube.

    * **Passo a Passo da Coleta:**
        1. Executar a análise do `phpmd` (com a ruleset `codesize`) no diretório `/app`, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd app/ xml codesize > phpmd_app_codesize.xml`

        2. Executar a análise do `phpmd` (com a ruleset `codesize`) no diretório `/src`, salvando a saída em XML: `docker compose exec horizon vendor/bin/phpmd src/ xml codesize > phpmd_src_codesize.xml`

        3. Filtrar o XML do `/app` (`phpmd_app_codesize.xml`) para extrair apenas as violações de CC (CyclomaticComplexity): `grep 'rule="CyclomaticComplexity"' phpmd_app_codesize.xml > cc_app.txt`

        4. Filtrar o XML do /`src` (`phpmd_src_codesize.xml`) para extrair apenas as violações de CC: `grep 'rule="CyclomaticComplexity"' phpmd_src_codesize.xml > cc_src.txt`

        5. Consolidar manualmente os dados dos arquivos `cc_app.txt` e `cc_src.txt` em uma planilha Excel (Diretório, Classe, Método, Valor CC).

        6. Iniciar o serviço do SonarQube para a coleta dos dados globais: `sudo systemctl start sonarqube`

        7. Acessar a interface do SonarQube (`http://localhost:9000`) e coletar a contagem total de "Funções" (Functions) e a "Complexidade Ciclomática" (Cyclomatic Complexity) total dos diretórios `/app` e `/src`.

    * **Dados Coletados:**
        * Nº Total de Métodos em `/app` e `/src`: 3450
        * Valor Total de CC em `/app` e `/src`: 5588
        * Nº de Métodos Capturados pelo `phpmd`: 34
        * Nº de Métodos Considerados Insatisfatórios: 23
        * Complexidade Ciclomática média por método: `Valor Total de CC em '/app' e '/src'/ Nº Total de Métodos em '/app' e '/src' =  1,62`
        * Número/Percentual de métodos com CC > 10: `(Nº de Métodos Insatisfatórios / Nº Total de métodos em '/app' e '/src')*100 = 0,67%` 

    * **Execução da Coleta**: Link para o vídeo da execução da coleta [Manutenibilidade - Métrica 2.1:  Complexidade Ciclomática (CC)](https://youtu.be/NKvr9xHC6bA)
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)


    ### Classificação da Métrica

    * **Resultado:** Média 1,62 / 0,67% dos métodos é "Insatisfatório"
    * **Critério (da Fase 2):**
        * Bom: CC ≤ 5
        * Regular: 5 < CC ≤ 10
        * Insatisfatório: CC > 10
    * **Classificação:** Bom

    ### Análise e Discussão

    A complexidade ciclomática (CC) do i-Educar é boa e o percentual de métodos que possuem uma complexidade ciclomática maior que 10, ou seja, insatisfatória para nossa análise, corresponde a menos de um por cento de todos os métodos coletados para a análise. Além disso, a média de CC por método também possui um valor bem abaixo do que definimos como "Bom" na definição das métricas. 
    
    Entretanto, cabe mencionar que alguns métodos capturados pelo phpmd na análise possuem um alto nível de CC, como o método "getExportFormatData" da classe "Registro10" em "/src" que possui uma CC de 186, demonstrando que apesar de em termos gerais a complexidade ciclomática ser boa, existem métodos que podem passar por análises pelo time de desenvolvimento do i-Educar visando diminuir a CC deles, como dito pela hipótese `H2.1`, um código com complexidade muito alta, faz o desenvolvedor gastar muito esforço cognitivo para entendê-lo.

??? "M3.1: Percentual de Cobertura de Teste (Line Coverage)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** Pest com Xdebug/PCOV.
    * **Comando:** `./vendor/bin/pest --coverage`
    
    * **Dados Coletados:**
        * Cobertura total de linhas (Line Coverage): 31.2%%

    * **Documento resultado da Coleta**: [coverage.odt](https://docs.google.com/document/d/1TqPZNILbWLGGVggxy26ZqZPHYV8Jh7kCiK3bIl_nB5M/edit?usp=sharing )
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)
    

    ### Classificação da Métrica

    * **Resultado:** 31.2%
    * **Critério (da Fase 2):**
        * Bom: ≥ 80%
        * Regular: 70% ≤ M3.1 < 80%
        * Insatisfatório: < 70%
    * **Classificação:** Insatisfatório

    ### Análise e Discussão

    A cobertura de teste de 31,2% classifica o projeto em um nível Insatisfatório, situando-se muito abaixo do limiar de segurança de 70-80% tipicamente recomendado para softwares em produção. Este indicador revela que mais de dois terços do código-fonte do i-Educar não são verificados pelas rotinas automatizadas de CI/CD, o que expõe o sistema a um risco elevado de regressões — ou seja, o surgimento de defeitos em funcionalidades antigas causados por novas alterações.

    No contexto específico do i-Educar, esse percentual reflete claramente a natureza híbrida do repositório. A baixa cobertura global é, muito provavelmente, o resultado de uma média ponderada entre o código moderno (nas pastas app e src), que tende a ser bem testado, e o vasto volume de código legado (na pasta ieducar), que historicamente carece de testes. Isso cria um cenário de "cobertura desigual": enquanto as novas funcionalidades desenvolvidas com práticas modernas (como o uso do Laravel e Pest) estão protegidas, o núcleo antigo do sistema permanece como uma "zona de sombra". Consequentemente, a equipe de desenvolvimento pode ter alta confiança ao refatorar componentes novos, mas deve manter cautela extrema ao tocar no legado, onde a ausência de testes automatizados exige um esforço manual de validação muito maior e mais propenso a erro humano.

??? "M3.2: Densidade de Testes (Testes/KLOC)"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `grep` e `cloc`.
    * **Dados Coletados:**
        * Nº total de testes (`grep -r "function test" tests/ | wc -l`): 1357
        * Linhas de código de produção totais (`cloc src/`): 142494
        * Cálculo: `(Nº Total de Testes / (Linhas Totais de Código / 1000))` = 9,523207995 Testes/KLOC

    * **Execução da Coleta**: [link para o vídeo com a execução da coleta](https://youtu.be/i_uHcweJ7zE)
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)

    ### Classificação da Métrica

    * **Resultado:** 9,523207995 Testes/KLOC
    * **Critério (da Fase 2):**
        * Bom: > 10 Testes/KLOC
        * Regular: 5 a 10 Testes/KLOC
        * Insatisfatório: < 5 Testes/KLOC
    * **Classificação:** Regular

    ### Análise e Discussão

    O projeto apresenta um comportamento que pode ser descrito como um “paradoxo” de qualidade, embora a Densidade de Testes seja classificada como Regular/Boa, a Cobertura de Código (vista na métrica anterior) permanece baixa, em apenas 31,2%. Esse contraste mostra algo comum em sistemas híbridos — a presença de uma “cobertura concentrada” ou até mesmo redundante. No caso do i-Educar, grande parte dos testes está provavelmente focada nos módulos modernos. Assim, áreas novas e bem cuidadas convivem com um grande volume de código antigo não testado, o que puxa a cobertura global para baixo e aumenta o risco operacional.

    Além disso, a quantidade elevada de testes pode estar focada em caminhos de sucesso (happy paths), resultando em múltiplas validações semelhantes e deixando de lado cenários de exceção e fluxos de erro que representam parte significativa da lógica existente. Também é possível que existam muitos testes superficiais, voltados para métodos simples (como getters e setters), enquanto trechos de código mais complexos, embora mais relevantes para a confiabilidade do sistema, recebem pouca atenção devido à dificuldade de criação de testes.

    Pela densidade, há, de fato, um esforço ativo de teste, mas ele está distribuído de forma desigual e não contribui de maneira eficiente para a solidez geral do sistema.

??? "M3.3: Tempo Médio de Execução dos Testes"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** Pest / Log do GitHub Actions.
    * **Dados Coletados:**
        * Tempo total de execução da suíte: 36.68s
        * Número total de testes(`grep -r "function test" tests/ | wc -l`): 1357
        * Cálculo (Tempo por teste): `(36.68 / 1357)` = 0.027s por teste

    * **Execução da Coleta**: [link para o vídeo com a execução da coleta](https://www.youtube.com/watch?v=p1CINURPWvc)
    * **Armazenamento dos Dados**: Planilha Excel - [Coleta de Dados i-Educar](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing)

    ### Classificação da Métrica

    * **Resultado:** 0.027s (Tempo médio por teste)
    * **Critério (da Fase 2):**
        * Bom: ≤ 1s
        * Regular: 1s < M3.3 ≤ 3s
        * Insatisfatório: > 3s
    * **Classificação:** Bom

    ### Análise e Discussão

    A análise do Tempo Médio de Execução dos testes teve um resultado bom: 0,027 segundos por caso de teste. Isso indica que a suíte é capaz de executar aproximadamente 37 testes por segundo, um desempenho acima do esperado para um sistema com características legadas como o i-Educar. A justificativa de que bateria de testes está surpreendentemente ágil pode refletir realmente poucos testes. Dá para perceber que a maior parte das validações automatizadas está concentrada nas porções modernas do código. Essas áreas utilizam boas práticas contemporâneas que favorecem a criação de testes unitários rápidos e isolados. Além disso, existe muito uso de mocks, stubs e bancos de dados em memória, estratégias que evitam operações de I/O e eliminam gargalos. O resultado também sugere a ausência de testes end-to-end, como os realizados com Dusk ou Selenium, que possuem tempos de execução significativamente maiores e poderiam elevar drasticamente a média geral.

    Em resumo, o tempo médio de 0,027 segundos demonstra que a suíte de testes é extremamente eficiente, mas também aponta para um foco excessivo em camadas específicas do sistema. Embora o desempenho seja excelente do ponto de vista técnico, ele também reforça a necessidade de ampliar a abrangência dos testes para incluir fluxos críticos de negócio e, futuramente, testes de integração mais robustos e testes end-to-end que validem o funcionamento do sistema de ponta a ponta.

---

## 4. Conclusão

Com base nos resultados obtidos nas seis métricas avaliadas, a característica Manutenibilidade do i-Educar foi classificada como **Parcialmente Aceitável**, conforme os Critérios de Julgamento definidos na [Fase 2](../fase_2/gqm_manutenibilidade.md). Metade das métricas apresentou desempenho Bom ou Excelente (acoplamento, complexidade e tempo de execução de testes), mas problemas críticos foram identificados na duplicação de código e na cobertura de testes.

A avaliação das três questões do GQM revela um cenário misto: a **Questão 1** sobre impacto das alterações apresenta resultados contraditórios, com baixo acoplamento (ponto forte), mas alta duplicação de código (ponto fraco crítico). A **Questão 2** sobre complexidade de entendimento foi respondida positivamente, com baixa complexidade geral, mas pontos pontuais de complexidade extrema. A **Questão 3** sobre situação dos testes apresenta um paradoxo: testes rápidos e densidade regular, mas cobertura insuficiente e desigual.

### Síntese das Avaliações

| Métrica | Resultado | Julgamento | Hipótese |
| ------- | --------- | ---------- | -------- |
| **M1.1 – Acoplamento (CBO)** | Média 18 / 1,70% classes insatisfatórias | Bom | H1.1 **parcialmente validada** |
| **M1.2 – Código Repetido** | 7,4% | Insatisfatório | H1.1 **validada** |
| **M2.1 – Complexidade Ciclomática** | Média 1,62 / 0,67% métodos insatisfatórios | Bom | H2.1 **parcialmente validada** |
| **M3.1 – Cobertura de Teste** | 31,2% | Insatisfatório | H3.1 **validada** |
| **M3.2 – Densidade de Testes** | 9,52 Testes/KLOC | Regular | N/A |
| **M3.3 – Tempo de Execução** | 0,027s por teste | Bom | H3.2 **invalidada** |

### Principais Pontos Fortes

* **Baixo Acoplamento (M1.1):** Apenas 1,70% das classes apresentam CBO insatisfatório (≥15), demonstrando que a arquitetura mantém baixa interdependência entre a maioria dos componentes. Isso facilita alterações isoladas e reduz o risco de efeitos colaterais em cascata.

* **Complexidade Controlada (M2.1):** A complexidade ciclomática média de 1,62 por método está muito abaixo do limiar de preocupação (5), indicando que a maior parte do código é compreensível e segue estruturas simples, facilitando a manutenção e o onboarding de novos desenvolvedores.

* **Testes Rápidos e Eficientes (M3.3):** O tempo médio de 0,027s por teste (37 testes/segundo) permite feedback instantâneo aos desenvolvedores, favorecendo práticas de desenvolvimento ágil e TDD. Isso demonstra uso eficiente de mocks, stubs e isolamento adequado dos testes unitários.

### Principais Pontos Fracos

* **Alta Duplicação de Código (M1.2):** Com 7,4% de código repetido distribuído em 2.485 blocos duplicados, qualquer correção ou melhoria exige retrabalho significativo em múltiplos pontos do sistema. Isso aumenta o esforço de manutenção, eleva o risco de inconsistências entre as cópias e dificulta a evolução do código.

* **Cobertura de Teste Insuficiente (M3.1):** Apenas 31,2% do código está coberto por testes, deixando mais de dois terços do sistema (68,8%) exposto a riscos de regressão. A baixa cobertura dificulta refatorações seguras, aumenta a dependência de testes manuais e compromete a confiança na estabilidade do sistema após alterações.

* **Distribuição Desigual de Testes (M3.1 + M3.2):** A densidade regular de testes (9,52 Testes/KLOC) combinada com baixa cobertura global evidencia o padrão de "cobertura concentrada": os módulos modernos (`/app` e `/src`) possuem testes rápidos e bem estruturados, enquanto o código legado (`/ieducar`) permanece praticamente sem proteção automatizada.

* **Complexidade Extrema Pontual (M2.1):** Embora a média seja baixa, a existência de métodos com CC extremamente alta — como `getExportFormatData` (CC=186) — representa "ilhas de complexidade" que dificultam significativamente a compreensão, manutenção e testabilidade desses pontos críticos.

### Avaliação Final

Diante da análise das métricas, a Manutenibilidade do i-Educar atinge o critério de **Parcialmente Aceitável** (50% das métricas classificadas como Bom ou Excelente). O sistema apresenta fundação sólida em design orientado a objetos, mas falhas críticas em cobertura de testes e duplicação de código comprometem a capacidade de manutenção sustentável a longo prazo.

A arquitetura híbrida do projeto cria uma dualidade clara: módulos modernos demonstram maturidade técnica (baixo acoplamento, baixa complexidade, testes rápidos), mas convivem com um vasto legado carente de cobertura de testes, propenso a duplicação e com pontos de complexidade extrema. Esta situação é típica de sistemas em transição, onde novas práticas são aplicadas em código novo, mas o legado permanece sem refatoração significativa.

**Recomendações para evolução para nível "Aceitável":**

1. **Refatoração sistemática de código duplicado:** Priorizar os 2.485 blocos identificados, criando abstrações reutilizáveis e eliminando redundância.
2. **Expansão gradual da cobertura de testes:** Focar inicialmente em módulos críticos do código legado (`/ieducar`), priorizando lógica de negócio essencial.
3. **Decomposição de métodos complexos:** Revisar e refatorar métodos com CC > 100, aplicando técnicas como Extract Method e Strategy Pattern.
4. **Manutenção das boas práticas:** Preservar os padrões estabelecidos nos módulos modernos, garantindo que novo código mantenha baixo acoplamento e complexidade controlada.

Em síntese, o i-Educar demonstra **maturidade técnica em design**, mas requer **investimento estruturado em qualidade de testes e eliminação de débito técnico** para garantir manutenibilidade sustentável, especialmente considerando sua natureza de software livre dependente de contribuições comunitárias.

---

## Referências Bibliográficas

> [1] CHIDAMBER, Shyam R.; KEMERER, Chris F. A Metrics Suite for Object Oriented Design. IEEE Transactions on Software Engineering, v. 20, n. 6, p. 476-493, jun. 1994.

> [2] PORTÁBILIS. i-Educar: Software livre de gestão escolar. Versão 2.10.0. [S.l.]: Portábilis Tecnologia, 2025. Disponível em: https://github.com/portabilis/i-educar. Acesso em: 17 nov. 2025.

> [3] MARTIN, Robert C. Clean Code: A Handbook of Agile Software Craftsmanship. Upper Saddle River, NJ: Prentice Hall, 2008.

> [4] MCCABE, Thomas J. A Complexity Measure. IEEE Transactions on Software Engineering, v. SE-2, n. 4, p. 308-320, dez. 1976.

> [5] BUGBUG. What is Test Coverage in Software Testing? BugBug Blog, 2024. Disponível em: https://bugbug.io/blog/software-testing/test-coverage/. Acesso em: 28 nov. 2025.

> [6] GRAPHITE. Measuring and Calculating Defect Density. Graphite Guides, 2024. Disponível em: https://graphite.com/guides/measuring-and-calculating-defect-density. Acesso em: 28 nov. 2025.

> [7] BECK, Kent. Test Driven Development: By Example. Boston: Addison-Wesley Professional, 2002.

> [8] SHORE, James; WARDEN, Shane. The Art of Agile Development. 2. ed. Sebastopol, CA: O'Reilly Media, 2021.