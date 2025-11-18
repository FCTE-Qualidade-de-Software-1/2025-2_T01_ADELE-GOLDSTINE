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

* **Cobertura de Teste e Densidade:** Explique o que é cobertura de linha e por que ela, sozinha, não é suficiente (daí a necessidade da "Densidade de Testes").

* **Tempo de Execução:** Por que testes lentos impactam o ciclo de desenvolvimento (CI/CD, feedback lento).

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

## 4. Conclusão (Manutenibilidade)

[PREENCHER: Faça uma conclusão *específica* para a Manutenibilidade.
* Com base nos resultados das 6 métricas, o objetivo de Manutenibilidade foi atingido?
* Use os "Critérios para Julgamento" da Fase 2 (Aceitável, Parcialmente aceitável, Inaceitável) para dar um veredito sobre esta característica.
* Quais foram os principais pontos fortes e fracos encontrados? (Ex: "A cobertura de teste é boa, mas a complexidade e o acoplamento são 'Insatisfatórios', indicando um código difícil de manter.")
* (Opcional) Quais hipóteses (H1.1, H2.1, H3.1, H3.2) foram validadas ou invalidadas pela coleta?]

---

## Referências Bibliográficas

> [1] CHIDAMBER, Shyam R.; KEMERER, Chris F. A Metrics Suite for Object Oriented Design. IEEE Transactions on Software Engineering, v. 20, n. 6, p. 476-493, jun. 1994.

> [2] PORTÁBILIS. i-Educar: Software livre de gestão escolar. Versão 2.10.0. [S.l.]: Portábilis Tecnologia, 2025. Disponível em: https://github.com/portabilis/i-educar. Acesso em: 17 nov. 2025.

> [3] MARTIN, Robert C. Clean Code: A Handbook of Agile Software Craftsmanship. Upper Saddle River, NJ: Prentice Hall, 2008.

> [4] MCCABE, Thomas J. A Complexity Measure. IEEE Transactions on Software Engineering, v. SE-2, n. 4, p. 308-320, dez. 1976.