## Análise Integrada e Diagrama Geral

A avaliação de qualidade de software raramente se restringe a características isoladas. As características definidas na ISO 25010, como Confiabilidade, Manutenibilidade e Segurança, são interdependentes. Uma melhoria em uma pode fortalecer outra, enquanto uma fraqueza em uma pode ser a causa-raiz de um problema em outra.

Esta página apresenta o diagrama GQM geral do projeto, consolidando os planos de medição das três características priorizadas. Mais importante, ela fornece uma análise das **sinergias** — as conexões onde métricas de uma característica ajudam a responder perguntas de outra, permitindo uma visão holística e profunda da qualidade do i-Educar.

## Diagrama GQM Integrado

O diagrama abaixo ilustra a decomposição GQM para Confiabilidade (G1), Manutenibilidade (G2) e Segurança (G3), destacando as conexões entre os planos.

!!! info
    Dê zoom com o scroll do mouse no diagrama para ver melhor. Caso prefira, abra em tela cheia.<br/>
    Você também mode mover o diagrama com o mouse.

``` mermaid
flowchart TB
 subgraph G1["G1: Avaliar Confiabilidade"]
        Q1_1["Q1.1: Qual é a estabilidade do código..."]
        M1_1["M1.1: Densidade de Defeitos"]
        M1_2["M1.2: Percentual de Commits de Correção"]
        Q1_2["Q1.2: Qual é o nível de robustez..."]
        M2_1["M2.1: Índice de Tratamento de Exceções"]
        Q1_3["Q1.3: Qual é a eficácia da recuperação..."]
        M3_1["M3.1: Análise Qualitativa de Backup"]
  end
 subgraph G2["G2: Avaliar Manutenibilidade"]
        Q2_1["Q2.1: Qual o impacto de realizar uma alteração..."]
        M1_1_Manu["M1.1: Coupling Between Objects (CBO)"]
        M1_2_Manu["M1.2: Percentual de Código Repetido"]
        Q2_2["Q2.2: Quão complexo é entender o código..."]
        M2_1_Manu["M2.1: Complexidade Ciclomática (CC)"]
        Q2_3["Q2.3: Como está a situação atual dos testes?"]
        M3_1_Manu["M3.1: Percentual de Cobertura de Teste"]
        M3_2_Manu["M3.2: Densidade de Testes"]
        M3_3_Manu["M3.3: Tempo Médio de Execução"]
  end
 subgraph G3["G3: Avaliar Segurança"]
        Q3_1["Q3.1: Qual é o nível de robustez do controle de acesso..."]
        M1_1_Seg["M1.1: % de rotas críticas com autorização"]
        M1_2_Seg["M1.2: Método de armazenamento de senhas"]
        M1_3_Seg["M1.3: Tempo médio de expiração da sessão"]
        Q3_2["Q3.2: Qual é o nível de rastreabilidade..."]
        M2_1_Seg["M2.1: % de ações críticas em logs"]
        M2_2_Seg["M2.2: % de logs com informações completas"]
        Q3_3["Q3.3: Em que medida o desenvolvimento segue práticas de segurança?"]
        M3_1_Seg["M3.1: Densidade de testes de segurança"]
        M3_2_Seg["M3.2: Frequência de atualização de dependências"]
  end
    Q1_1 --> M1_1 & M1_2
    Q1_2 --> M2_1
    Q1_3 --> M3_1
    Q2_1 --> M1_1_Manu & M1_2_Manu
    Q2_2 --> M2_1_Manu
    Q2_3 --> M3_1_Manu & M3_2_Manu & M3_3_Manu
    Q3_1 --> M1_1_Seg & M1_2_Seg & M1_3_Seg
    Q3_2 --> M2_1_Seg & M2_2_Seg
    Q3_3 --> M3_1_Seg & M3_2_Seg
    Goal0["G0: Aplicação do Método GQM para avaliação de qualidade do software i-Educar"] --> G1 & G2 & G3
    M2_1_Seg -.-> Q1_2 & Q1_3
    M2_2_Seg -.-> Q1_2 & Q1_3
    M2_1_Manu -.-> Q1_2
    M3_1_Seg -.-> Q2_3
    M3_2_Manu -.-> Q2_3
    linkStyle 16 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 17 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 18 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 19 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 20 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 21 stroke:#aaa,stroke-dasharray: 5 5,fill:none
    linkStyle 22 stroke:#aaa,stroke-dasharray: 5 5,fill:none


```

-----

## Análise das Sinergias

A verdadeira força desta avaliação GQM está nas conexões entre os planos. Elas revelam como a qualidade de uma característica é, muitas vezes, dependente de outra.

### 1\. Sinergia: Logs de Segurança Robustez e Recuperabilidade (Confiabilidade)

  * **Conexão:** As métricas `Segurança - M2.1` (Percentual de ações críticas registradas em logs) e `Segurança - M2.2` (Percentual de logs com informações completas) são essenciais para responder às questões `Confiabilidade - Q2` (Qual é o nível de robustez...) e `Confiabilidade - Q3` (Qual é a eficácia dos mecanismos de recuperação...).
  * **Motivação (Por quê?):** A Confiabilidade não se resume a *evitar* falhas; ela também mede a capacidade do sistema de *lidar* com falhas (Tolerância a Falhas) e se *recuperar* delas (Recuperabilidade). No contexto de um desenvolvedor, quando uma falha inesperada ocorre, a primeira (e muitas vezes única) ferramenta de diagnóstico são os logs do sistema.
  * **Implicação:** Se as métricas de Segurança (`Segurança - M2.1`, `Segurança - M2.2`) forem "Insatisfatórias", a capacidade do sistema de ser robusto (`Confiabilidade - Q2`) e recuperável (`Confiabilidade - Q3`) é, na prática, quase nula. Um problema de Confiabilidade pode ter sua causa-raiz em uma falha de Segurança (monitoramento).

### 2\. Sinergia: Complexidade (Manutenibilidade) e Robustez (Confiabilidade)

  * **Conexão:** A métrica `Manutenibilidade - M2.1` (Complexidade Ciclomática) tem um impacto direto na questão `Confiabilidade - Q2` (Robustez).
  * **Motivação (Por quê?):** A "robustez" (`Confiabilidade - Q2`) é frequentemente medida pela capacidade do código de lidar com entradas inesperadas ou falhas de I/O, o que é feito via tratamento de exceções (`Confiabilidade - M2.1`). No entanto, código com alta Complexidade Ciclomática (`Manutenibilidade - M2.1` > 10) possui muitos caminhos de execução.
  * **Implicação:** É exponencialmente mais difícil garantir que *todos* os caminhos de um método complexo tenham o tratamento de exceção adequado. Uma alta complexidade lógica (Manutenibilidade) quase sempre leva a uma baixa robustez (Confiabilidade), pois caminhos de erro são esquecidos.

### 3\. Sinergia: Densidade de Testes (Manutenibilidade) vs. Densidade de Testes (Segurança)

  * **Conexão:** A `Manutenibilidade - Q3` (Como está a situação atual dos testes?) só pode ser respondida de forma completa ao comparar as métricas de teste de Manutenibilidade e Segurança.
  * **Motivação (Por quê?):** A questão `Manutenibilidade - Q3` avalia a qualidade da suíte de testes. Uma métrica isolada como `Manutenibilidade - M3.1` (Cobertura de Teste) pode ser enganosa — um projeto pode ter 90% de cobertura de linha e ainda assim não testar nenhuma vulnerabilidade de segurança.
  * **Implicação:** A "situação dos testes" (`Manutenibilidade - Q3`) só é compreendida quando combinamos a cobertura (`Manutenibilidade - M3.1`) com a densidade geral de testes (`Manutenibilidade - M3.2`) e a densidade específica de testes de segurança (`Segurança - M3.1`). Esta conexão expõe potenciais "pontos cegos": a suíte de testes pode ser boa para lógica de negócio (alta densidade em `Manutenibilidade - M3.2`), mas péssima para Segurança (baixa densidade em `Segurança - M3.1`).

### Conclusão da Análise

Este modelo GQM integrado demonstra que as características de qualidade não são silos. A análise cruzada permite identificar causas-raiz (ex: um problema de **Confiabilidade** pode ser causado por alta **Manutenibilidade**) e otimizar esforços (ex: melhorar os logs de **Segurança** beneficia diretamente a **Confiabilidade**).