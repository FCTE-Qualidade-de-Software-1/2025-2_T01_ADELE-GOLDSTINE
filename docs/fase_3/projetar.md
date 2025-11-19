# Fase 3 - Projetar a Avaliação

## Plano de Avaliação

Avaliar a **Confiabilidade, Manutenibilidade e Segurança** do sistema i-Educar, com base no plano de medição GQM (Goal-Question-Metric) definido na Fase 2. O objetivo é executar a coleta de dados de forma sistemática para identificar pontos de vulnerabilidade, débito técnico e riscos operacionais, validando as hipóteses formuladas.

## 1. Método de Avaliação

Será utilizada uma abordagem mista (quantitativa e qualitativa) baseada no plano GQM. A coleta de dados combinará ferramentas de análise estática de código, análise de histórico de repositório e inspeção manual de código para as métricas qualitativas.

| **Dimensão** | **Questão (GQM)** | **Métrica (GQM)** | **Ferramenta / Fonte de Dados** | **Como Utilizar (Plano de Coleta)** |
| --- | --- | --- | --- | --- |
| **Confiabilidade** | Q1.1: Estabilidade do código? | M1.1: Densidade de Defeitos | API do GitHub, `cloc` | 1. Listar `issues` com label `bug` criadas nos últimos 12 meses ou total do projeto. <br> 2. Contar KLOC de código PHP com `cloc`. <br> 3. Aplicar a fórmula: `(Issues / KLOC)`. |
| | | M1.2: % Commits de Correção | `git log` | 1. Contar total de commits: `git log --oneline --no-merges`. <br> 2. Contar commits de correção: `git log --grep="fix\|corrige\|bug" --no-merges`. <br> 3. Aplicar a fórmula. |
| | Q1.2: Robustez contra falhas? | M2.1: Índice de Tratamento de Exceções | Análise Estática (`grep`), Revisão Manual | 1. Definir operações críticas (ex: `pg_connect`, `new PDO`). <br> 2. Contar o total de ocorrências. <br> 3. Contar quantas estão sintaticamente dentro de um bloco `try-catch`. |
| | Q1.3: Eficácia da recuperação? | M3.1: Análise Qualitativa de Código de Backup | Revisão Manual (Checklist) | 1. Localizar as rotinas de backup no código. <br> 2. Aplicar o checklist (0-10 pontos) definido na Fase 2 (documentação, clareza, tratamento de erros, etc.). |
| **Manutenibilidade** | Q2.1: Impacto das alterações? | M1.1: Coupling Between Objects (CBO) | `phpmd` ou SonarQube | 1. Executar a ferramenta sobre o código-fonte. <br> 2. Obter o valor médio de CBO para as classes e identificar classes com CBO > 15. |
| | | M1.2: Percentual de Código Repetido | `phpcpd` ou SonarQube | 1. Executar a ferramenta sobre o código-fonte. <br> 2. Obter o percentual de linhas de código duplicadas. |
| | Q2.2: Complexidade de entendimento? | M2.1: Complexidade Ciclomática (CC) | `phpmd` ou SonarQube | 1. Executar a ferramenta. <br> 2. Identificar a média de CC por método e a quantidade de métodos com CC > 10. |
| | Q2.3: Situação dos testes? | M3.1: Percentual de Cobertura de Teste | PHPUnit, Xdebug/PCOV | 1. Executar a suíte de testes com cobertura (ex: `phpunit --coverage-clover`). <br> 2. Extrair o percentual total de linhas cobertas do relatório. |
| | | M3.2: Densidade de Testes (Testes/KLOC) | `grep`, `cloc` | 1. Contar nº total de testes: `grep -r "function test" tests/`. <br> 2. Contar KLOC total de produção. <br> 3. Calcular `(Nº Testes / KLOC)`. |
| | | M3.3: Tempo Médio de Execução dos Testes | PHPUnit / GitHub Actions | 1. Registrar o tempo de execução da suíte completa de testes no pipeline de CI ou localmente. <br> 2. Dividir pelo número de testes para obter a média. |
| **Segurança** | Q3.1: Robustez do controle de acesso? | M1.1: % de rotas críticas com autorização | Revisão Manual (Código) | 1. Listar rotas/módulos críticos (ex: Notas, Alunos). <br> 2. Inspecionar se possuem regras de autorização/middleware aplicadas. <br> 3. Calcular o percentual protegido. |
| | | M1.2: Método de armazenamento de senhas | Revisão Manual (Código) | 1. Localizar o código de autenticação/criação de usuário. <br> 2. Verificar se utiliza hash seguro (ex: `password_hash`, bcrypt) ou inseguro (MD5, SHA1). |
| | | M1.3: Tempo médio de expiração da sessão | Revisão Manual (Config) | 1. Inspecionar arquivos de configuração (`session.gc_maxlifetime` ou `.env`). <br> 2. Verificar o tempo configurado em minutos. |
| | Q3.2: Rastreabilidade das ações? | M2.1: % de ações críticas em logs | Revisão Manual, `grep` | 1. Listar ações críticas (login, delete, update). <br> 2. Inspecionar o código e verificar quais geram registro de log. |
| | | M2.2: % de logs com informações completas | Revisão Manual (Amostragem) | 1. Coletar uma amostra de logs gerados. <br> 2. Verificar o percentual que contém (Usuário, Ação, Data/Hora). |
| | Q3.3: Práticas de dev seguro? | M3.1: Densidade de testes de segurança | `grep`, `cloc` | 1. Contar testes específicos de segurança na suíte. <br> 2. Contar KLOC total de produção. <br> 3. Calcular densidade: `(Nº Testes Seg / KLOC)`. |
| | | M3.2: Frequência de atualização de dependências | Histórico do Git (`composer.lock`) | 1. Analisar o histórico de commits do arquivo de dependências. <br> 2. Calcular o tempo médio (em meses) entre atualizações. |

---

### 2. Recursos Necessários

| Recurso | Descrição |
| --- | --- |
| **Ferramentas (CLI)** | `git`, `cloc`, `grep` (ou `ack`), `phpmd` (PHP Mess Detector), `phpcpd` (PHP Copy/Paste Detector), `phpunit`. |
| **Plataformas** | Acesso à API do GitHub (para issues) e ao pipeline de CI (GitHub Actions, para tempo de teste). |
| **Ambiente** | Ambiente local com o código-fonte do i-Educar clonado e as dependências (PHP, Composer) instaladas para execução das ferramentas. |
| **SonarQube (Opcional)** | Alternativa robusta que substitui `phpmd`, `phpcpd` e `cloc` com uma única análise, se a equipe optar por configurá-lo. |

---

### 3. Cronograma de Ações

O cronograma será focado na coleta paralela dos dados de cada característica, seguida por uma fase de consolidação e análise.

| Etapa (Agrupada por Característica) | Métricas Coletadas | Responsável(eis) | Prazo Estimado |
| :--- | :--- | :--- | :--- |
| **Configuração do Ambiente** | Instalação de ferramentas (phpmd, cloc, etc.) | Todos | Dia 1 |
| **Coleta de Confiabilidade** | M1.1: Densidade de Defeitos <br> M1.2: % Commits de Correção <br> M2.1: Índice de Tratamento de Exceções <br> M3.1: Análise Qualitativa de Backup | Marcos | Dias 1-3 |
| **Coleta de Manutenibilidade** | M1.1: Acoplamento (CBO) <br> M1.2: % Código Repetido <br> M2.1: Complexidade Ciclomática (CC) <br> M3.1: Cobertura de Teste <br> M3.2: Densidade de Testes <br> M3.3: Tempo de Execução dos Testes | Manuella <br> Andre | Dias 1-3 |
| **Coleta de Segurança** | M1.1: % Rotas c/ Autorização <br> M1.2: Armazenamento de Senhas <br> M1.3: Expiração de Sessão <br> M2.1: % Ações em Logs <br> M2.2: % Logs Completos <br> M3.1: Densidade de Testes de Segurança <br> M3.2: Frequência de Atualização | Caio Antonio <br> Zenilda | Dias 1-3 |
| **Consolidação dos Dados** | Tabulação de todos os dados brutos em local central. | Todos | Dia 4 |
| **Análise e Relatório** | Aplicação das pontuações GQM e redação do relatório final da Fase 3. | Todos | Dia 5 |

### 4. Fontes de Evidência e Rastreabilidade

Os seguintes documentos e fontes serão usados para garantir a rastreabilidade e a veracidade da avaliação:

| **Fonte** | **Local/Ferramenta** | **Uso** | **Avaliação Esperada** |
| --- | --- | --- | --- |
| **Código-Fonte (i-Educar)** | [Repositório Oficial do i-Educar (GitHub)](https://github.com/portabilis/i-educar) | Fonte primária para todas as métricas de análise de código (estática e manual). | Os dados brutos (ex: contagens, trechos de código) serão extraídos desta fonte. |
| **Histórico (i-Educar)** | Repositório Oficial (Git Log, Issues) | Fonte primária para métricas de processo (commits, issues, atualizações). | Os dados (contagens, datas) serão extraídos desta fonte. |
| **Definição da Avaliação** | [Fase 2 - GQM](../fase_2/introducao_gqm.md) | Define formalmente cada métrica, o método de coleta e as pontuações de julgamento. | O plano de coleta (Seção 1) deve ser 100% fiel ao GQM da Fase 2. |
| **Dados Brutos Coletados** | [Fase 4 - GQM](../fase_4/introducao-avaliacao.md) e [Planilha de Avaliação](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?hl=pt-br&gid=0#gid=0) | Armazenamento dos resultados brutos. | Garante a auditabilidade e rastreabilidade da avaliação. |
| **Relatório Final** | [Relatório]() | Documento final que consolida os dados, aplica as pontuações e apresenta as conclusões. | O relatório deve referenciar os dados brutos. |

-----

## Histórico de Versão

| Data  |   Versão   | Descrição                                                             | Autor(es)                                    | Revisor(es)        |
| :---: | :--------: | :-------------------------------------------------------------------- | :------------------------------------------- | :----------------- |  
| `1.0` | 10/11/2025 | Criação do plano de avaliação da Fase 3.                              | [Marcos Marinho](https://github.com/devMarcosVM)                               | [Manuella Valadares](https://github.com/manuvaladares)  |
| `1.1` | 10/11/2025 | Revisão dos itens Método de Avaliação e Cronograma de Ações                               | [Zenilda Vieira](https://github.com/ZenildaVieira)                               |  |
| `1.2` | 11/11/2025 | Revisão do plano e adição das fontes e evidências de rastreabilidade. | [Manuella Valadares](https://github.com/manuvaladares) |                    |
| `1.3` | 16/11/2025 | Adequação ao novo escopo de avaliação                                 | [André Maia](http://github.com/andre-maia51) |                    |