# Avaliação da Confiabilidade

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Confiabilidade** do i-Educar.

## 1. Introdução

O objetivo definido para essa avaliação foi analisar o i-Educar com foco na Confiabilidade do ponto de vista da comunidade de desenvolvedores utilizando o GQM na definição das questões, hipóteses e métricas.

A avaliação da confiabilidade é fundamental para o i-Educar devido à sua função crítica na gestão escolar de instituições públicas e privadas. Como um sistema que gerencia dados sensíveis de estudantes, professores e processos educacionais, falhas podem resultar em perda de informações, interrupção de serviços essenciais e comprometimento da continuidade das operações escolares. A natureza híbrida do sistema, que combina código legado com implementações modernas, exige monitoramento constante da estabilidade e robustez para garantir que o software opere de forma previsível e resiliente.

Tendo isso em vista, a investigação foi guiada por três questões fundamentais definidas na [fase 2](../fase_2/gqm_confiabilidade.md) do processo de avaliação de qualidade de software:

1. **Maturidade (Q1):** Avalia a estabilidade do código em relação à ocorrência de defeitos, investigando a densidade de bugs reportados e o percentual de commits dedicados a correções.
2. **Tolerância a Falhas (Q2):** Mensura o nível de robustez do código contra falhas em tempo de execução, verificando a presença de mecanismos de tratamento de exceções em operações críticas.
3. **Recuperabilidade (Q3):** Avalia a eficácia dos mecanismos de recuperação de dados do sistema através de análise qualitativa do código de backup e restore.

## 2. Referencial Teórico

* **Maturidade do Software:** A maturidade refere-se ao grau de estabilidade e previsibilidade de um sistema de software em relação à ocorrência de defeitos [5]. Um software maduro apresenta baixa frequência de falhas e necessita de menos correções reativas. A **Densidade de Defeitos** (bugs por mil linhas de código) é uma métrica amplamente utilizada para quantificar a qualidade interna do código, permitindo comparações entre projetos de diferentes tamanhos [6]. O **Percentual de Commits de Correção** complementa essa análise ao revelar a proporção do esforço de desenvolvimento dedicado a corrigir problemas existentes versus desenvolver novas funcionalidades, sendo um indicador do caráter reativo ou proativo da equipe de desenvolvimento.

* **Tolerância a Falhas:** Tolerância a falhas é a capacidade de um sistema continuar operando corretamente mesmo quando ocorrem erros ou condições anormais [7]. Em sistemas de software, isso é frequentemente implementado através de **tratamento de exceções**, um mecanismo que permite ao programa detectar, capturar e responder a situações de erro de forma controlada, evitando crashes e comportamentos imprevisíveis. O **Índice de Tratamento de Exceções** mede a cobertura de operações críticas (como I/O de banco de dados e arquivos) por blocos try-catch, sendo um proxy da robustez do sistema frente a falhas operacionais.

* **Recuperabilidade:** Recuperabilidade é a capacidade do software de restabelecer seu nível de desempenho e recuperar dados afetados em caso de falha [8]. Para sistemas que gerenciam dados críticos, como o i-Educar, mecanismos confiáveis de backup e restore são essenciais. A **Análise Qualitativa de Código de Backup** avalia aspectos como documentação, clareza, tratamento de erros, externalização de configurações e testabilidade das rotinas de backup, fatores que impactam diretamente a manutenibilidade e confiabilidade desses componentes críticos em cenários de recuperação de desastre.

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Confiabilidade.

???+ "M1.1: Densidade de Defeitos no Código"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** API do GitHub (Search API) e `cloc`.
    * **Comandos executados (executados dentro do diretório `i-educar`):**
        * Obter o remote do repositório: `git remote get-url origin` → `git@github.com:portabilis/i-educar.git`
        * Contagem de linhas PHP: `cloc --json .` → PHP code = 203217 linhas
        * Contagem de issues com label `bug` (GitHub Search API):
          `curl -s "https://api.github.com/search/issues?q=repo:portabilis/i-educar+label:bug+type:issue" | python3 -c "import sys,json; print(json.load(sys.stdin).get('total_count',0))"` → `74`

    * **Dados Coletados:**
        * Número total de issues com a label `bug`: 74 (open + closed; obtido via GitHub Search API)
        * Total de linhas de código (PHP): 203.217 LOC → 203.217 KLOC (contados em `.` — diretório do repositório `i-educar`)
        * Cálculo: `(74 / 203.217)` = 0.364 bugs/KLOC (aprox.)

    * **Evidência da coleta (vídeo):**
    
    <iframe width="560" height="315" src="https://www.youtube.com/embed/SQXXsj0_fPU?si=nBMmah9c4phw-rQ-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

    ### Classificação da Métrica

    * **Resultado:** 0.364 bugs/KLOC
    * **Critério (da Fase 2):**
        * Excelente: ≤ 1 bug/KLOC
        * Bom: >1 e ≤3 bugs/KLOC
        * Regular: >3 e ≤6 bugs/KLOC
        * Insatisfatório: >6 bugs/KLOC
    * **Classificação:** Excelente

    ### Análise e Discussão

    O índice calculado (aprox. 0.364 bugs/KLOC) é baixo e, segundo os critérios definidos na Fase 2, coloca o repositório na faixa "Excelente" (≤ 1 bug/KLOC). Na prática, isso significa que, em termos de issues rotuladas como `bug` por unidade de tamanho do código, o i-Educar apresenta uma densidade de defeitos reportados relativamente pequena.

    Sobre a hipótese H1.1 ("A densidade de defeitos geral do sistema será superior a 3 bugs/KLOC"): a hipótese é **invalidada** pelos dados coletados — o valor observado (≈0.364 bugs/KLOC) é muito inferior ao limiar de 3 bugs/KLOC. Isso indica que, com base nas issues rotuladas e na contagem de linhas PHP, não há um passivo de defeitos reportados na magnitude esperada por H1.1.

??? "M1.2: Percentual de Commits de Correção"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `git` 
    * **Comandos executados:**
        * Total de commits (sem merges):
          `git log --oneline --no-merges | wc -l` → `22582`
        * Commits de correção (mensagens contendo: fix|corrige|bugfix|hotfix|patch):
          `git log --grep="fix\|corrige\|bugfix\|hotfix\|patch" --regexp-ignore-case --oneline --no-merges | wc -l` → `1929`

    * **Dados Coletados:**
        * Total de commits: 22.582
        * Commits de correção (heurística por palavra-chave): 1.929
        * Cálculo: `(1.929 / 22.582) * 100` = 8.55% (aprox.)

    * **Evidência da coleta (vídeo):**
    
    <iframe width="560" height="315" src="https://www.youtube.com/embed/J5sr0SFpObI?si=DvRSH1mRRYofIlRR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

    ### Classificação da Métrica

    * **Resultado:** 8.55%
    * **Critério (da Fase 2):**
        * Excelente: ≤ 10%
        * Bom: >10% e ≤20%
        * Regular: >20% e ≤35%
        * Insatisfatório: >35%
    * **Classificação:** Excelente

    ### Análise e Discussão

    O percentual de commits de correção encontrado (≈ 8.55%) indica que menos de 10% dos commits correspondem a mensagens com termos associados a correções, o que, segundo os critérios definidos, coloca o projeto na faixa "Excelente" para essa métrica.

    Sobre a hipótese H1.2 ("O percentual de commits de correção será superior a 15%"), a hipótese é **invalidada** pelos dados coletados: o percentual observável (≈8.55%) está bem abaixo do limiar de 15%, sugerindo que a maior parte do esforço de desenvolvimento não está sendo registrada como commits de correção via as palavras-chave escolhidas. Em conjunto com a baixa densidade de defeitos (M1.1), isso dá indício de que o projeto possui estabilidade relativa.

??? "M2.1: Índice de Tratamento de Exceções"

    ### Evidências e Dados Brutos

    * **Ferramenta(s):** `grep` (heurística por arquivo; executado dentro do diretório `i-educar`)
    * **Operações críticas definidas:** `new PDO(`, `pg_connect(`, `fopen(`, `file_put_contents(`, `curl_exec(`, `fsockopen(`
    * **Comandos executados (coleta em 19 Nov 2025, dentro de `/home/marcos/Documentos/i-educar`):**
        * Contar ocorrências (linhas) de operações críticas:
          `grep -R --line-number --include="*.php" -E "new PDO\(|pg_connect\(|fopen\(|file_put_contents\(|curl_exec\(|fsockopen\(" . 2>/dev/null | wc -l` → `6`
        * Arquivos únicos com operações críticas:
          `grep -R --include="*.php" -l -E "new PDO\(|pg_connect\(|fopen\(|file_put_contents\(|curl_exec\(|fsockopen\(" . 2>/dev/null | sort -u > /tmp/files_io_ieducar.txt`
          `wc -l /tmp/files_io_ieducar.txt` → `5`
        * Arquivos com blocos `try`:
          `grep -R --include="*.php" -l -E "try\s*\{" . 2>/dev/null | sort -u > /tmp/files_try_ieducar.txt`
          `wc -l /tmp/files_try_ieducar.txt` → `95`
        * Arquivos com ambas as características (aproximação):
          `comm -12 /tmp/files_io_ieducar.txt /tmp/files_try_ieducar.txt | wc -l` → `1`

    * **Dados Coletados:**
        * Número total de ocorrências (linhas) de operações críticas: 6
        * Número de arquivos únicos que contêm operações críticas: 5
        * Número de arquivos com blocos `try`: 95
        * Número de arquivos com ambas (I/O + try): 1
        * Cálculo aproximado (por arquivo): `(1 / 5) * 100` = 20.0%

    * **Evidência da coleta (vídeo):**
    
    <iframe width="560" height="315" src="https://www.youtube.com/embed/-zk3bTqagT4?si=sPhRWzBngIZUcuPc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

    ### Classificação da Métrica

    * **Resultado:** 20.0% (aproximação por arquivo)
    * **Critério (da Fase 2):**
        * Excelente: ≥ 90%
        * Bom: 70%–89%
        * Regular: 40%–69%
        * Insatisfatório: < 40%
    * **Classificação:** Insatisfatório

    ### Análise e Discussão

    O índice de tratamento de exceções calculado (20.0%) indica que apenas 1 dos 5 arquivos PHP que contêm operações críticas de I/O também possui blocos `try`, o que coloca a métrica na faixa "Insatisfatório" segundo os critérios estabelecidos.

    Sobre a hipótese H2.1 ("Menos de 50% das operações críticas de I/O possuirão tratamento adequado de exceções"): a hipótese é **validada** pelos dados coletados — o percentual observado (20%) está bem abaixo de 50%, indicando deficiência na cobertura de tratamento de exceções nas operações de I/O detectadas. No entanto, é importante considerar que o código moderno do i-Educar utiliza abstrações do Laravel (Eloquent, Storage, HTTP client) que já possuem tratamento interno de exceções.

??? "M3.1: Análise Qualitativa de Código de Backup"

    ### Evidências e Dados Brutos

    * **Método:** Inspeção manual do código (executado dentro do diretório `i-educar`)
    * **Comandos de localização executados:**
        * Busca por referências a backup/restore/dump:
          `grep -R -n --exclude-dir=vendor --exclude-dir=node_modules -i "backup\|restore\|dump" . 2>/dev/null | head -n 50`
        * Busca de arquivos com nomes relacionados:
          `find . -type f \( -iname "*backup*" -o -iname "*restore*" -o -iname "*dump*" \) -not -path "*/vendor/*" -not -path "*/node_modules/*" 2>/dev/null`
    
    * **Arquivos identificados (módulo de backup/restore):**
        * `app/Console/Commands/DatabaseRestoreCommand.php` (121 linhas) — comando CLI para restauração de banco
        * `app/Http/Controllers/BackupController.php` (17 linhas) — controller para download de backups
        * `app/Services/BackupUrlPresigner.php` (18 linhas) — serviço para geração de URLs pré-assinadas
        * `app/Services/S3BackupUrlPresigner.php` — implementação específica para S3
        * `app/Models/Backup.php` (21 linhas) — modelo Eloquent para registro de backups
        * `ieducar/intranet/educar_backup_lst.php` — listagem de backups (código legado)
        * `database/migrations/legacy/2020_01_01_110000_create_pmieducar_backup_table.php` — migration da tabela
        * `tests/Unit/Eloquent/BackupTest.php` — testes unitários do modelo

    * **Checklist de Análise (Pontuação 0-2) — aplicado ao arquivo principal `DatabaseRestoreCommand.php`:**
        * **Documentação (Comentários):** 2/2
            - Possui docblocks PHPDoc em todos os métodos públicos e privados explicando propósito, parâmetros e retorno.
            - Comentários claros sobre a operação (ex.: "Drop old database if exists and create it again").
        * **Clareza do Código (Nomes de variáveis e métodos):** 2/2
            - Nomes autoexplicativos: `dropAndCreateDatabase`, `restoreDatabaseUsingBackupFile`, `getHost`, `getPort`, `getUser`.
            - Estrutura bem organizada em métodos pequenos e focados (Single Responsibility Principle).
        * **Tratamento de Erros:** 0/2
            - Nenhum tratamento de exceções ou validação de erros explícito.
            - Uso de `passthru()` sem captura ou verificação de código de retorno, o que pode resultar em falha silenciosa se o comando `pg_restore` ou `psql` falhar.
            - Não há validação de existência do arquivo de backup antes de tentar restaurar.
        * **Configuração (Externalizada vs. Hard-coded):** 2/2
            - Configurações críticas (host, porta, usuário) são lidas de variáveis de ambiente via `env()`.
            - Sem credenciais ou caminhos hard-coded no código.
        * **Testabilidade:** 1/2
            - Estrutura modular com métodos privados bem separados facilita testes unitários (mock de `passthru`).
            - Porém, uso de funções globais (`passthru`, `env`) dificulta isolamento em testes sem preparação adicional.
            - Existe arquivo de teste (`BackupTest.php`), mas apenas para o modelo `Backup`, não para o comando de restore.
    * **Cálculo (Soma):** 7 / 10

    * **Evidência da coleta (vídeo):**
    
    <iframe width="560" height="315" src="https://www.youtube.com/embed/7DVlzixS87Q?si=-Cdm04zhjcyeVTSH" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

    ### Classificação da Métrica

    * **Resultado:** 7 / 10
    * **Critério (da Fase 2):**
        * Excelente: 9–10
        * Bom: 7–8
        * Regular: 4–6
        * Insatisfatório: 0–3
    * **Classificação:** Bom

    ### Análise e Discussão

    A análise qualitativa do código de backup/restore do i-Educar resultou em uma pontuação de 7/10, classificada como "Bom" segundo os critérios estabelecidos. O código possui documentação adequada, nomenclatura clara e estrutura modular, seguindo boas práticas do Laravel (uso correto de variáveis de ambiente para configurações).

    No entanto, o ponto crítico identificado foi a **ausência total de tratamento de erros** nas operações de shell (`pg_restore`, `psql` via `passthru()`). Não há verificação de códigos de retorno ou validação de existência de arquivos antes da restauração, o que representa um risco operacional em cenários de desastre — falhas podem ocorrer silenciosamente, resultando em perda de dados ou restauração incompleta.

    Sobre a hipótese H3.1 ("A análise qualitativa das rotinas de backup revelará uma baixa pontuação de manutenibilidade, inferior a 5 em 10"): a hipótese é **invalidada** pelos dados coletados — a pontuação observada (7/10) está acima do limiar de 5, indicando manutenibilidade aceitável do código de backup. 

---

## 4. Conclusão (Confiabilidade)

Com base nos resultados das quatro métricas coletadas, a **Confiabilidade do i-Educar** é classificada como **Aceitável**. Seguindo os critérios estabelecidos na Fase 2 (sistema aceitável se pelo menos 70% das métricas atingirem "Bom" ou "Excelente"), observamos que 75% das métricas (3 de 4) alcançaram esses níveis:

- **M1.1 - Densidade de Defeitos:** 0,364 bugs/KLOC (Excelente)
- **M1.2 - Percentual de Commits de Correção:** 8,55% (Excelente)
- **M2.1 - Índice de Tratamento de Exceções:** 20% (Insatisfatório)
- **M3.1 - Qualidade do Código de Backup:** 7/10 (Bom)

**Principais pontos fortes identificados:**

- **Maturidade elevada:** densidade de defeitos muito baixa (0,364 bugs/KLOC) indica código estável e robusto, bem abaixo do limiar de 3 bugs/KLOC para sistemas aceitáveis.
- **Baixo percentual de commits corretivos:** apenas 8,55% dos commits são correções de bugs, demonstrando que a maior parte do esforço de desenvolvimento está concentrada em novas funcionalidades e melhorias, não em remediação de defeitos.
- **Código de backup manutenível:** a pontuação de 7/10 na análise qualitativa indica estrutura modular, documentação adequada e uso correto de boas práticas do Laravel.

**Principal ponto fraco crítico:**

- **Tolerância a falhas deficiente:** o índice de tratamento de exceções extremamente baixo (20%) revela que poucas operações críticas de I/O possuem proteção explícita contra falhas. Embora o Laravel forneça abstrações com tratamento interno, o código legado (`ieducar/`) e operações de shell (backup/restore via `passthru()`) não possuem validação ou captura de erros, o que representa risco operacional em cenários de desastre.

**Validação das hipóteses:**

- **H1.1 (invalidada):** a densidade de defeitos (0,364 bugs/KLOC) está **abaixo** do limiar de 3 bugs/KLOC previsto, indicando maturidade superior à esperada.
- **H1.2 (invalidada):** o percentual de commits de correção (8,55%) está **abaixo** dos 15% previstos, reforçando a maturidade do código.
- **H2.1 (validada):** confirmou-se que menos de 50% das operações críticas possuem tratamento de exceções adequado (apenas 20%), validando a preocupação com tolerância a falhas.
- **H3.1 (invalidada):** a qualidade do código de backup (7/10) está **acima** do limiar de 5/10 previsto, indicando recuperabilidade razoável.

**Recomendações prioritárias:**

1. **Melhorar tratamento de exceções:** adicionar blocos `try/catch` e validação de entrada em operações de I/O, especialmente no código legado e nas rotinas de backup/restore.
2. **Validação de operações de shell:** implementar verificação de códigos de retorno em comandos `passthru()` utilizados nas rotinas de backup, com notificação de falhas.
3. **Revisão do código legado:** mapear e refatorar operações críticas no diretório `ieducar/` que ainda não possuem tratamento de erros adequado.

Em síntese, o i-Educar demonstra **alta maturidade e estabilidade**, mas apresenta **vulnerabilidade operacional** devido à baixa cobertura de tratamento de exceções. A manutenção de um sistema confiável requer atenção especial à robustez das operações críticas, garantindo que falhas de infraestrutura (banco de dados, sistema de arquivos, rede) sejam tratadas graciosamente sem comprometer a integridade dos dados educacionais.

---

## Referências Bibliográficas

> [1] ISO/IEC 25010:2011. Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. International Organization for Standardization, 2011.

> [2] PORTÁBILIS. i-Educar: Software livre de gestão escolar. Versão 2.10.0. [S.l.]: Portábilis Tecnologia, 2025. Disponível em: https://github.com/portabilis/i-educar. Acesso em: 17 nov. 2025.

> [3] IEEE Std 829-2008. IEEE Standard for Software and System Test Documentation. Institute of Electrical and Electronics Engineers, 2008.

> [4] PRESSMAN, Roger S.; MAXIM, Bruce R. Software Engineering: A Practitioner's Approach. 9th ed. New York: McGraw-Hill Education, 2020.

> [5] SOMMERVILLE, Ian. Software Engineering. 10th ed. Boston: Pearson, 2016.

> [6] SPINELLIS, Diomidis. Code Quality: The Open Source Perspective. Boston: Addison-Wesley Professional, 2006.

> [7] BASS, Len; CLEMENTS, Paul; KAZMAN, Rick. Software Architecture in Practice. 3rd ed. Boston: Addison-Wesley Professional, 2012.

> [8] JØRGENSEN, Magne. Software Reliability: Measurement, Prediction, Application. Boston: Academic Press, 2016.
