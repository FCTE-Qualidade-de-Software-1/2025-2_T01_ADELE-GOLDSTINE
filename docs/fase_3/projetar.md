# Fase 3 - Projetar a Avaliação

## Plano de Avaliação

Avaliar a **Confiabilidade, Manutenibilidade e Segurança** do sistema i-Educar, com base no plano de medição GQM (Goal-Question-Metric) definido na Fase 2. O objetivo é executar a coleta de dados de forma sistemática para identificar pontos de vulnerabilidade, débito técnico e riscos operacionais, validando as hipóteses formuladas.

## 1\. Método de Avaliação

Será utilizada uma abordagem mista (quantitativa e qualitativa) baseada no plano GQM. A coleta de dados combinará ferramentas de análise estática de código, análise de histórico de repositório e inspeção manual de código para as métricas qualitativas.

| **Dimensão** | **Questão (GQM)** | **Métrica (GQM)** | **Ferramenta / Fonte de Dados** | **Como Utilizar (Plano de Coleta)** |
| --- | --- | --- | --- | --- |
| **Confiabilidade** | Q1.1: Estabilidade do código? | M1.1: Densidade de Defeitos | API do GitHub, `cloc` | 1. Listar `issues` com label `bug` criadas nos últimos 12 meses. <br> 2. Contar KLOC de código PHP com `cloc`. <br> 3. Aplicar a fórmula: `(Issues / KLOC)`. |
| | | M1.2: % Commits de Correção | `git log` | 1. Contar total de commits: `git log --oneline --no-merges`. <br> 2. Contar commits de correção: `git log --grep="fix\|corrige\|bug" --no-merges`. <br> 3. Aplicar a fórmula. |
| | Q1.2: Robustez contra falhas? | M1.3: Índice de Tratamento de Exceções | Análise Estática (`grep`), Revisão Manual | 1. Definir operações críticas (ex: `pg_connect`, `new PDO`). <br> 2. Contar o total de ocorrências. <br> 3. Contar quantas estão sintaticamente dentro de um bloco `try-catch`. |
| | Q1.3: Eficácia da recuperação? | M1.4: Análise Qualitativa de Backup | Revisão Manual (Checklist) | 1. Localizar as rotinas de backup no código. <br> 2. Aplicar o checklist (0-10 pontos) definido na Fase 2 (documentação, clareza, etc.). |
| **Manutenibilidade** | Q2.1: Impacto das alterações? | M2.1: Acoplamento (CBO) | `phpmd` ou SonarQube | 1. Executar a ferramenta sobre o código-fonte. <br> 2. Obter o valor médio de CBO para as classes e/ou identificar classes com CBO \> 15. |
| | | M2.2: % Código Repetido | `phpcpd` ou SonarQube | 1. Executar a ferramenta sobre o código-fonte. <br> 2. Obter o percentual de linhas de código duplicadas. |
| | Q2.2: Complexidade de entendimento? | M2.3: Complexidade Ciclomática (CC) | `phpmd` ou SonarQube | 1. Executar a ferramenta. <br> 2. Identificar a média de CC por método e a quantidade de métodos com CC \> 10. |
| | Q2.3: Situação dos testes? | M2.4: Cobertura de Teste (Linha) | PHPUnit, Xdebug/PCOV | 1. Executar a suíte de testes com cobertura (ex: `phpunit --coverage-clover`). <br> 2. Extrair o percentual total de linhas cobertas do relatório. |
| | | M2.5: Densidade de Testes | `grep`, `cloc` | 1. Contar nº de testes: `grep -r "function test" tests/`. <br> 2. Contar KLOC de produção. <br> 3. Calcular (Testes / KLOC). |
| | | M2.6: Tempo de Execução dos Testes | PHPUnit / GitHub Actions | 1. Registrar o tempo de execução da suíte completa de testes no pipeline de CI. |
| **Segurança** | Q3.1: Robustez do controle de acesso? | M3.1: % Módulos c/ Autorização | Revisão Manual (Código) | 1. Listar os principais módulos de negócio. <br> 2. Inspecionar se os controladores/rotas possuem checagens de permissão/papel. |
| | | M3.2: Armazenamento de Senhas | Revisão Manual (Código) | 1. Localizar o código de criação/login de usuário. <br> 2. Verificar se `password_hash()` e `password_verify()` (ou similar seguro) são utilizados. |
| | | M3.3: Expiração de Sessão | Revisão Manual (Config) | 1. Inspecionar arquivos de configuração do PHP/framework pelo tempo de vida da sessão (`session.gc_maxlifetime`). |
| | Q3.2: Rastreabilidade das ações? | M3.4: % Ações em Logs | Revisão Manual, `grep` | 1. Listar ações críticas (login, delete, update). <br> 2. Inspecionar o código e verificar quais delas geram uma entrada de log. |
| | | M3.5: % Logs Completos | Revisão Manual (Amostragem) | 1. Coletar uma amostra de 20-30 entradas de log de ações críticas. <br> 2. Verificar o percentual que contém (Usuário, Ação, Timestamp). |
| | Q3.3: Práticas de dev seguro? | M3.6: Testes de Segurança | `grep`, Revisão Manual | 1. Inspecionar a suíte de testes. <br> 2. Contar testes que validam falhas de permissão ou simulam entradas maliciosas. |
| | | M3.7: Frequência de Atualização | Histórico do Git (`composer.lock`) | 1. Analisar o histórico de commits do arquivo `composer.lock`. <br> 2. Calcular o tempo médio (em meses) entre atualizações de dependências. |

-----

### 2\. Recursos Necessários

| Recurso | Descrição |
| --- | --- |
| **Ferramentas (CLI)** | `git`, `cloc`, `grep` (ou `ack`), `phpmd` (PHP Mess Detector), `phpcpd` (PHP Copy/Paste Detector), `phpunit`. |
| **Plataformas** | Acesso à API do GitHub (para issues) e ao pipeline de CI (GitHub Actions, para tempo de teste). |
| **Ambiente** | Ambiente local com o código-fonte do i-Educar clonado e as dependências (PHP, Composer) instaladas para execução das ferramentas. |
| **SonarQube (Opcional)** | Alternativa robusta que substitui `phpmd`, `phpcpd` e `cloc` com uma única análise, se a equipe optar por configurá-lo. |

-----

### 3\. Cronograma de Ações

O cronograma será focado na coleta paralela dos dados de cada característica, seguida por uma fase de consolidação e análise.

| Etapa (Agrupada por Característica) | Métricas Coletadas | Responsável(eis) | Prazo Estimado |
| :--- | :--- | :--- | :--- |
| **Configuração do Ambiente** | Instalação de ferramentas (phpmd, cloc, etc.) | Todos | Dia 1 |
| **Coleta de Confiabilidade** | M1.1: Densidade de Defeitos <br> M1.2: % Commits de Correção <br> M1.3: Índice de Tratamento de Exceções <br> M1.4: Análise Qualitativa de Backup | Marcos | Dias 1-3 |
| **Coleta de Manutenibilidade** | M2.1: Acoplamento (CBO) <br> M2.2: % Código Repetido <br> M2.3: Complexidade Ciclomática (CC) <br> M2.4: Cobertura de Teste <br> M2.5: Densidade de Testes <br> M2.6: Tempo de Execução dos Testes | Manuella <br> Andre | Dias 1-3 |
| **Coleta de Segurança** | M3.1: % Módulos c/ Autorização <br> M3.2: Armazenamento de Senhas <br> M3.3: Expiração de Sessão <br> M3.4: % Ações em Logs <br> M3.5: % Logs Completos <br> M3.6: Testes de Segurança <br> M3.7: Frequência de Atualização | Caio Antonio <br> Zenilda | Dias 1-3 |
| **Consolidação dos Dados** | Tabulação de todos os dados brutos em local central. | Todos | Dia 4 |
| **Análise e Relatório** | Aplicação das pontuações GQM e redação do relatório final da Fase 3. | Todos | Dia 5 |

### 4\. Fontes de Evidência e Rastreabilidade

Os seguintes documentos e fontes serão usados para garantir a rastreabilidade e a veracidade da avaliação:

| **Fonte** | **Local/Ferramenta** | **Uso** | **Avaliação Esperada** |
| --- | --- | --- | --- |
| **Código-Fonte (i-Educar)** | Repositório Oficial do i-Educar (GitHub) | Fonte primária para todas as métricas de análise de código (estática e manual). | Os dados brutos (ex: contagens, trechos de código) serão extraídos desta fonte. |
| **Histórico (i-Educar)** | Repositório Oficial (Git Log, Issues) | Fonte primária para métricas de processo (commits, issues, atualizações). | Os dados (contagens, datas) serão extraídos desta fonte. |
| **Definição da Avaliação** | Repositório da Disciplina (Fase 2 - GQM) | Define formalmente cada métrica, o método de coleta e as pontuações de julgamento. | O plano de coleta (Seção 1) deve ser 100% fiel ao GQM da Fase 2. |
| **Dados Brutos Coletados** | Repositório da Disciplina (ex: `/dados_fase3/`) | Armazenamento dos resultados brutos (planilhas, logs das ferramentas, screenshots). | Garante a auditabilidade e rastreabilidade da avaliação. |
| **Relatório Final** | Repositório da Disciplina (Fase 3) | Documento final que consolida os dados, aplica as pontuações e apresenta as conclusões. | O relatório deve referenciar os dados brutos. |

-----

## Histórico de Versão

| Data | Versão | Descrição | Autor(es) | Data de revisão | Revisor(es) |
| :---: | :----: | :---: | :---: | :---: | :---: |
| 10/11/2025 | `1.0` | Criação do plano de avaliação da Fase 3. | Marcos Marinho | | |
| | | | | | |