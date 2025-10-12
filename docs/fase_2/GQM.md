
# Abordagem GQM

A metodologia GQM (Goal-Question-Metric) foi empregada para estruturar a avaliação de qualidade do software i-Educar, com foco na característica de Confiabilidade. A escolha desta característica foi motivada por inúmeros relatos de profissionais da educação sobre instabilidades e falhas no sistema, o que a torna um ponto crítico para a usabilidade e eficácia do produto em seu ambiente de operação.

A abordagem GQM garante que as métricas coletadas estejam diretamente alinhadas aos objetivos da avaliação, transformando um problema de negócio (baixa confiabilidade percebida) em um plano de medição concreto e orientado a dados.

1. **Objetivo (Goal):** Define o que se deseja alcançar, considerando o propósito, o objeto de estudo, o ponto de vista e o contexto.
2. **Perguntas (Questions):** Identificam os aspectos específicos que precisam ser avaliados para atingir o objetivo.
3. **Métricas (Metrics):** Fornecem os dados necessários para responder às perguntas, permitindo uma análise quantitativa ou qualitativa.

Essa metodologia é especialmente útil em projetos complexos, onde a medição de características como confiabilidade, manutenibilidade e segurança é essencial para garantir o sucesso do sistema.

## Objetivo de Medição 1: Confiabilidade

**Tabela 1** - Objetivo de Medição 1: Confiabilidade.

| **Analisar**          | o i-Educar |
|------------------------|------------|
| **Para o propósito de** | Identificar e caracterizar pontos do código que possam causar falhas|
| **Com respeito a**     | Confiabilidade |
| **Do ponto de vista da** | Comunidade de desenvolvedores do i-Educar |
| **No contexto da**     | Disciplina de Qualidade de Software |

---

### Perguntas e Hipóteses de Medição

Para decompor o objetivo de análise da Confiabilidade, foram formuladas as seguintes perguntas e hipóteses. As hipóteses tornam explícito o conhecimento atual sobre o sistema, que será validado pelas métricas.

**Questão 1: Maturidade**
> Com que frequência o código existente gera defeitos?

* **Hipótese 1.1 (H1.1):** Os módulos de maior importância para o negócio (**Escola**, **Servidores** e **Educacenso**) apresentarão uma **densidade de defeitos** (bugs por KLOC) pelo menos 20% superior à média dos demais módulos do sistema.

* **Hipótese 1.2 (H1.2):** O **percentual de commits de correção** no histórico do projeto será superior a 15%, indicando que uma parcela significativa do esforço de desenvolvimento é reativa, focada na correção de falhas existentes.

**Questão 2: Tolerância a Falhas**
> O código está preparado para lidar com erros inesperados durante a execução?

* **Hipótese 2.1 (H2.1):** Menos de 50% das operações críticas de entrada/saída (I/O), como conexões com banco de dados e manipulação de arquivos nos módulos priorizados, possuirão um mecanismo adequado de tratamento de exceções (try-catch).

**Questão 3: Recuperabilidade**
> O sistema possui mecanismos de recuperação de dados que um desenvolvedor possa verificar e manter?

* **Hipótese 3.1 (H3.1):** A **análise qualitativa das rotinas de backup** revelará uma baixa pontuação de manutenibilidade (inferior a 5 em 10), devido à falta de documentação clara e à complexidade do código, representando um risco para a manutenção desses mecanismos.

---

### Seleção das Métricas

**Questão 1: Maturidade**

* **Métrica 1.1: Densidade de Defeitos no Código**
    * **Definição:** Número de *issues* com a label `bug` no repositório GitHub, normalizado por mil linhas de código (KLOC).
    * **Fórmula:** `(Número total de issues "bug") / (Total de linhas de código / 1000)`
    * **Coleta:** 
        1. Listar todas as issues com a label `bug` via API do GitHub ou busca manual.
        2. Contar as linhas de código PHP (`.php`) para os módulos priorizados (Escola, Servidores, Educacenso) e para o restante do sistema separadamente, utilizando a ferramenta `cloc`.
        3. Aplicar a fórmula para os dois escopos (prioritários vs. não prioritários) e comparar os resultados para validar a **H1.1**.
    * **Propósito:** Identificar se as áreas mais críticas do sistema são também as que concentram mais defeitos reportados.

* **Métrica 1.2: Percentual de Commits de Correção**

    * **Definição:** Percentual de **commits** cuja mensagem contém palavras-chave como "fix", "corrige" ou "bugfix".
    * **Fórmula:** `(Número de commits de correção / Número total de commits) * 100`
    * **Coleta:**
        1. Definir um período de análise (ex: últimos 24 meses).
        2. Contar o número total de commits com `git log --oneline | wc -l`
        3. Contar o número de commits de correção com `git log --grep="fix\|bugfix\|corrige\|correção\|hotfix" --regexp-ignore-case --oneline | wc -l.`
        4. Aplicar a fórmula para validar a **H1.2**.
    * **Propósito:** Avaliar se o esforço de desenvolvimento é mais reativo (corrigindo falhas) do que proativo (desenvolvendo novas funcionalidades).

**Questão 2: Tolerância a Falhas**

* **Métrica 2.1: Índice de Tratamento de Exceções**

    * **Definição:** Percentual de operações de I/O críticas que estão contidas dentro de um bloco de tratamento de exceções (`try-catch`).
    * **Fórmula:** `(Número de operações críticas com try-catch / Número total de operações críticas) * 100`
    * **Coleta:** Revisão manual de código ou uso de scripts de análise estática para buscar padrões de tratamento de exceções.
        1. Definir a lista de "operações críticas": chamadas de função/método para conexão com banco de dados ex:( `new PDO(`, `pg_connect`), manipulação de arquivos (ex: `fopen`, `file_put_contents`) etc.
        2. Nos diretórios dos módulos priorizados, executar scripts de busca (`grep` ou `ack`) para contar o número total de ocorrências dessas operações.
        3. Executar um segundo script para contar quantas dessas ocorrências estão sintaticamente dentro de um bloco `try { ... }`.
        4. Aplicar a fórmula para validar a **H2.1**.
    * **Propósito:** Medir a robustez do código contra erros em tempo de execução.

**Questão 3: Recuperabilidade**

* **Métrica 3.1: Análise Qualitativa de Código de Backup**

    * **Definição:** Avaliação qualitativa, baseada em um checklist estruturado, das rotinas de backup para verificar sua compreensibilidade, documentação e aderência a boas práticas.
    * **Coleta:** Inspeção manual do código-fonte das funcionalidades de backup.
        1. Identificar os arquivos/módulos responsáveis pela funcionalidade de backup/restauração no código-fonte.
        2. Realizar uma inspeção manual do código aplicando o checklist abaixo. Cada item recebe uma nota de 0 (ausente) a 2 (excelente).
        3. Checklist de Análise:
            * **Documentação (Comentários):** O código possui comentários explicando a lóǵica geral e os passos críticos?
            * **Clareza do Código:** Os nomes de variáveis e funções são intuitivos e seguem um padrão?
            * **Tratamento de Erros:** O código verifica falhas potenciais (ex: falha de escrita em disco, permissões) e as reporta de forma adequada?
            * **Configuração:** As configurações críticas (ex: caminhos de backup, credenciais) são externalizadas e não "hard-coded"?
            * **Testabilidade:** A estrutura do código permite a criação de testes unitários ou de integração?
        4. A pontuação final (0 a 10) será a soma dos pontos do checklist, usada para validar a **H3.1**.
    * **Propósito:** Avaliar a manutenibilidade e a confiabilidade percebida dos mecanismos de recuperação de dados do ponto de vista de um desenvolvedor.

---

### Relação entre a Confiabilidade, Perguntas e Métricas

![Relação entre a Confiabilidade, Perguntas e Métricas](../assets/diagrama_confiabilidade.png)

<p align="center"><b>Figura 1</b> - Diagrama ilustrando a relação entre a característica de Confiabilidade, as perguntas formuladas e as métricas definidas na abordagem GQM.</p>

<!-- AQUI IRIAM OS OUTROS OBJETIVOS DE MEDIÇÃO (MANUTENIBILIDADE E SEGURANÇA) COM SUAS RESPECTIVAS TABELAS, PERGUNTAS, HIPÓTESES, MÉTRICAS E DIAGRAMAS

pensei que esse próximo tópico poderia ser o mesmo para os 3 objetivos de medição, já que a gente vai usar os mesmos níveis de pontuação e critérios de julgamento para todos, então ele fica no final -->

## Níveis de Pontuação e Critérios de Julgamento

Para cada métrica definida por meio da abordagem GQM, foram estabelecidos níveis de pontuação que permitem interpretar os resultados de maneira padronizada, facilitando comparações e decisões. Esses níveis foram definidos com base em referências da literatura, benchmarks de ferramentas de análise estática e boas práticas de engenharia de software.

A seguir, apresenta-se a escala de pontuação definida pela equipe:

| Desempenho da Métrica | Pontuação | Interpretação Qualitativa |
| :--- | :---: | :--- |
| **Excelente** | 9 - 10 | Atende ou supera as expectativas de qualidade. Indica um código saudável e alinhado às boas práticas. |
| **Bom** | 7 - 8 | Atende de forma satisfatória, com pequenas e pontuais oportunidades de melhoria. |
| **Regular** | 4 - 6 | Apresenta deficiências perceptíveis que podem indicar débito técnico ou risco moderado. |
| **Insatisfatório** | 1 - 3 | Compromete significativamente a característica de qualidade, exigindo atenção e provável refatoração. |

### Critérios para Julgamento

Com base nas métricas e nos níveis de pontuação definidos, foram estabelecidos critérios de julgamento para interpretar os resultados da avaliação e apoiar a tomada de decisões. Os critérios são organizados por característica e baseiam-se na média de desempenho das métricas associadas a cada uma delas.

#### Critérios para Confiabilidade
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O sistema demonstra robustez e previsibilidade.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. O sistema funciona, mas pode apresentar instabilidades pontuais.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". A estabilidade do sistema é considerada crítica e propensa a falhas.

#### Critérios para Manutenibilidade
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O código é considerado claro, organizado e com baixo custo de manutenção.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. A manutenção é possível, mas com esforço considerável devido ao débito técnico.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". O código é de difícil compreensão e modificação, desestimulando novas contribuições.

#### Critérios para Segurança
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O sistema adere às boas práticas de codificação segura.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. Foram identificadas vulnerabilidades de baixo ou médio risco.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". Existem vulnerabilidades críticas que comprometem a integridade ou a confidencialidade dos dados.
