## Objetivo de Medição 2: Manutenibilidade

<div align="center">
  <table border="1" cellspacing="0" cellpadding="8" style="border-collapse: collapse; text-align: left;">
    <tr>
      <th><b>Analisar</b></th>
      <td>o i-Educar</td>
    </tr>
    <tr>
      <th><b>Para o propósito de</b></th>
      <td>Avaliar</td>
    </tr>
    <tr>
      <th><b>Com respeito a</b></th>
      <td>Manutenibilidade</td>
    </tr>
    <tr>
      <th><b>Do ponto de vista da</b></th>
      <td>Equipe de desenvolvimento</td>
    </tr>
    <tr>
      <th><b>No contexto da</b></th>
      <td>Disciplina de Qualidade de Software 1 (FCTE - UnB)</td>
    </tr>
  </table>

  <div style="margin-top: 8px; text-align: center;">
    <font size="4"><figcaption>Tabela 3: Objetivo de Medição: Manutenibilidade</figcaption></font>
  </div>
</div>

---

### Perguntas e Hipóteses de Medição

Para decompor o objetivo de análise da Manutenibilidade, foram formuladas as seguintes perguntas e hipóteses.

**Questão 1: Impacto das Alterações**
> Qual o impacto de realizar uma alteração no sistema?

* **Hipótese 1.1 (H1.1):** Códigos com alto acoplamento (CBO > 15) e alta duplicação de código (M2 > 5%) estão correlacionados a um aumento no tempo de implementação de correções, pois causam efeitos colaterais inesperados.

**Questão 2: Complexidade de Entendimento**
> Quão complexo é entender o código-fonte do i-Educar?

* **Hipótese 2.1 (H2.1):** Um código estruturalmente complexo (Complexidade Ciclomática > 10) aumenta o tempo necessário para um novo desenvolvedor entender onde e como realizar uma alteração.

**Questão 3: Cobertura de Testes**
> Como está a situação atual dos testes do i-Educar?

* **Hipótese 3.1 (H3.1):** Módulos com baixa cobertura de teste (M3.1 < 70%) apresentarão uma maior probabilidade de introdução de bugs de regressão em produção.
* **Hipótese 3.2 (H3.2):** O tempo médio de execução dos testes (M3.3 > 3s) é considerado alto pela equipe, desincentivando a execução frequente da suíte de testes during o desenvolvimento.

---

### Seleção das Métricas

**Questão 1: Impacto das Alterações**

* **Métrica 1.1: Coupling Between Objects (CBO)**
    * **Definição:** Mede o número de outras classes às quais uma classe está acoplada (depende). Um valor alto indica que a classe é altamente dependente e modificá-la pode impactar muitas outras partes do sistema.
    * **Coleta:** Análise estática do código-fonte (ex: `phpmd` ou SonarQube) para calcular o CBO para cada classe.
    * **Pontuação de Julgamento:**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | CBO ≤ 10 | 10 < CBO ≤ 15 | CBO > 15 |

    * **Propósito:** Avaliar o nível de acoplamento. Um CBO baixo é desejável, pois indica melhor modularidade e menor risco de propagação de defeitos.

* **Métrica 1.2: Percentual de Código Repetido**
    * **Definição:** Percentual de linhas de código que são idênticas ou muito similares a outros blocos de código no projeto.
    * **Coleta:** Análise estática utilizando ferramentas de detecção de duplicação (ex: `phpcpd` ou SonarQube).
    * **Pontuação de Julgamento:**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | M1.2 ≤ 3% | 3% < M1.2 ≤ 5% | M1.2 > 5% |

    * **Propósito:** Medir a quantidade de código duplicado ("copy-paste"). A duplicação aumenta o custo de manutenção, pois correções e alterações precisam ser feitas em múltiplos lugares.

**Questão 2: Complexidade de Entendimento**

* **Métrica 2.1: Complexidade Ciclomática (CC)**
    * **Definição:** Mede o número de caminhos linearmente independentes através do código-fonte de uma função ou método. Quantifica a complexidade lógica do código.
    * **Coleta:** Análise estática por função/método (ex: `phpmd` ou SonarQube).
    * **Pontuação de Julgamento:**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | CC ≤ 5 | 5 < CC ≤ 10 | CC > 10 |

    * **Propósito:** Identificar métodos e funções que são difíceis de entender, testar e manter.

**Questão 3: Cobertura de Testes**

* **Métrica 3.1: Percentual de Cobertura de Teste (Line Coverage)**
    * **Definição:** Percentual de linhas de código executáveis que são de fato executadas pela suíte de testes automatizados.
    * **Coleta:** Execução da suíte de testes (ex: PHPUnit) com a ferramenta de geração de relatório de cobertura habilitada (ex: Xdebug, PCOV).
    * **Pontuação de Julgamento:**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | M3.1 ≥ 80% | 70% ≤ M3.1 < 80% | M3.1 < 70% |

    * **Propósito:** Medir o grau em que o código-fonte é testado, indicando a confiança contra regressões.

* **Métrica 3.2: Densidade de Testes por Módulo (Testes/KLOC)**
    * **Definição:** Número de casos de teste automatizados para cada mil linhas de código (KLOC) de produção de um módulo (Escola, Servidores, Educacenso).
    * **Coleta:** 
        1.  Contar o número de testes para o Módulo X (ex: `grep -r "function test" tests/ModuleX | wc -l`).
        2.  Contar as linhas de código de produção do Módulo X (ex: `cloc src/ModuleX` e pegar o valor de "code").
        3.  Calcular a densidade: `(Número de Testes / (Linhas de Código / 1000))`
    * **Pontuação de Julgamento (Sugestão):**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | > 10 Testes/KLOC | 5 a 10 Testes/KLOC | < 5 Testes/KLOC |

    * **Propósito:** Avaliar se o esforço de teste está distribuído proporcionalmente à complexidade e ao tamanho do módulo, garantindo que módulos maiores tenham uma quantidade correspondente de validações.

* **Métrica 3.3: Tempo Médio de Execução dos Testes**
    * **Definição:** Tempo médio (em segundos) para a execução de um único caso de teste automatizado, ou da suíte inteira. (Nota: Critérios provavelmente referem-se ao tempo médio *por teste*).
    * **Coleta:** Medição do tempo de execução do pipeline de CI (ex: GitHub Actions) ou localmente.
    * **Pontuação de Julgamento:**

      | Bom | Regular | Insatisfatório |
      |:---|:---|:---|
      | M3.3 ≤ 1s | 1s < M3.3 ≤ 3s | M3.3 > 3s |

    * **Propósito:** Avaliar a eficiência da suíte de testes. Testes lentos desestimulam os desenvolvedores a executá-los com frequência.

---

### Critérios de Julgamento para Manutenibilidade

* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O código é considerado claro, organizado e com baixo custo de manutenção.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. A manutenção é possível, mas com esforço considerável devido ao débito técnico.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". O código é de difícil compreensão e modificação, desestimulando novas contribuições.

---

### Relação entre a Manutenibilidade, Perguntas e Métricas

<div align="center">
  <table border="1" cellspacing="0" cellpadding="8" style="border-collapse: collapse; text-align: left;">
    <tr>
      <th><b>Questão</b></th>
      <th><b>Métricas Simplificadas</b></th>
      <th><b>Tipo de Coleta</b></th>
    </tr>
    <tr>
      <td>1 – Impacto das Alterações </td>
      <td>M1.1: CBO; M1.2: Código Repetido</td>
      <td>Análise Estática</td>
    </tr>
    <tr>
      <td>2 – Complexidade de Entendimento</td>
      <td>M2.1: Complexidade Ciclomática</td>
      <td>Análise Estática</td>
    </tr>
    <tr>
      <td>3 – Cobertura de Testes</td>
      <td>M3.1: Cobertura de Teste; M3.2: Densidade de Testes; M3.3: Tempo de Execução</td>
      <td>Análise Estática / Execução de Testes</td>
    </tr>
  </table>

  <div style="margin-top: 8px; text-align: center;">
    <font size="4"><figcaption>Tabela 4: Questões e Métricas Simplificadas</figcaption></font>
  </div>
</div>

---

### Diagrama GQM - Manutenibilidade (Representação Estrutural)

![Diagrama GQM - Manutenibilidade](../assets/diagrama_manutenibilidade.png)

<div align="center">
  <font size="4"><figcaption>Figura 3: Diagrama GQM - Manutenibilidade. Autor: <a href="http://github.com/andre-maia51">André Maia</figcaption></font>
</div>