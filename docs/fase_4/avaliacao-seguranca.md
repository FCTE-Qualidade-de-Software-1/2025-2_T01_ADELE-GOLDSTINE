# Avaliação da Segurança

Esta página apresenta a execução da avaliação e os resultados da coleta de dados para o objetivo GQM de **Segurança** do i-Educar.

## 1. Introdução

[PREENCHER: Faça uma breve introdução sobre este objetivo.
* Qual era o objetivo (Goal) GQM definido na Fase 2 para Segurança?
* Por que avaliar a segurança é crítico neste software (LGPD, dados sensíveis de menores de idade)?
* Quais questões principais (Controle de Acesso, Monitoramento/Auditoria, Desenvolvimento Seguro) foram investigadas?]

## 2. Referencial Teórico

[PREENCHER: Apresente a base teórica *para as métricas* que serão mostradas.
* **Controle de Acesso (OWASP):** Explique o que é "Broken Access Control" (OWASP A1) e como as métricas de Autorização (M1.1) e Expiração de Sessão (M1.3) se relacionam a isso.
* **Armazenamento Criptográfico (OWASP):** Explique "Cryptographic Failures" (OWASP A2), a importância de usar *hashing* moderno (como `password_hash` / bcrypt) em vez de `md5()` (M1.2).
* **Logs e Monitoramento (OWASP):** Explique "Insufficient Logging & Monitoring" (OWASP A9) e por que não basta logar (M2.1), é preciso logar *informações completas* (M2.2).
* **Desenvolvimento Seguro:** Defina o que são testes de segurança (M3.1) e por que "Vulnerable and Outdated Components" (OWASP A6) é um risco (M3.2 - Frequência de Atualização).
* Lembre-se de citar as fontes (OWASP Top 10, LGPD, etc.).]

---

## 3. Coleta e Análise das Métricas

Aqui são apresentados os dados brutos, a classificação e a análise individual de cada métrica de Segurança.

???+ "Métrica 1.1: Percentual de módulos com regras de autorização"

    ### Evidências e Dados Brutos

    * **Método:** Revisão de código fonte e documentação.
    * **Módulos sensíveis analisados:** [PREENCHER: Ex: Gestão de Alunos, Gestão de Notas, Gestão de Servidores]
    * **Dados Coletados:**
        * Total de módulos sensíveis: [PREENCHER]
        * Módulos com checagem de autorização por papel: [PREENCHER]
        * Cálculo: `([Com Autorização] / [Total]) * 100` = [VALOR FINAL]%

    ![Exemplo de verificação de autorização no código]
    ![Exemplo de módulo sem verificação de autorização]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Excelente: ≥ 90%
        * Bom: 70% a 89%
        * Regular: 40% a 69%
        * Insatisfatório: < 40%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que esse percentual indica? Um valor baixo é uma falha crítica de segurança (Broken Access Control). Significa que um usuário com permissão baixa (ex: professor) poderia acessar dados de outro nível (ex: administrador). Isso valida H1.1?]

??? "Métrica 1.2: Método de armazenamento de senhas"

    ### Evidências e Dados Brutos

    * **Método:** Análise de código fonte (Localização: [PREENCHER CAMINHO]).
    * **Funções procuradas:** `md5()`, `sha1()`, `password_hash()`, `password_verify()`.
    * **Dado Coletado:** O sistema utiliza [PREENCHER: ex: `md5()` ou `password_hash()`] para armazenar senhas.

    ![Código de armazenamento de senha]

    ### Classificação da Métrica

    * **Resultado:** Utiliza [NOME DA FUNÇÃO]
    * **Critério (da Fase 2):**
        * Conforme: (Uso de `password_hash()` ou similar moderno)
        * Não conforme: (Uso de `md5()`, `sha1()` ou texto plano)
    * **Classificação:** [PREENCHER: Conforme/Não conforme]

    ### Análise e Discussão

    [PREENCHER: Isso valida a H1.2? Se for "Não conforme" (ex: usa MD5), as senhas dos usuários estão em risco extremo em caso de vazamento de banco de dados. Se for "Conforme", o sistema segue as boas práticas.]

??? "Métrica 1.3: Tempo médio de expiração da sessão"

    ### Evidências e Dados Brutos

    * **Método:** Análise de arquivos de configuração (ex: `.env`, `config.php`) ou teste funcional.
    * **Parâmetro analisado:** `session.gc_maxlifetime` (ou equivalente do framework).
    * **Dado Coletado:** Tempo de expiração configurado: [VALOR FINAL] minutos.

    ![Arquivo de configuração da sessão]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL] minutos
    * **Critério (da Fase 2):**
        * Conforme: Menor ou igual a 60
        * Não conforme: Acima de 60
    * **Classificação:** [PREENCHER: Conforme/Não conforme]

    ### Análise e Discussão

    [PREENCHER: Isso valida a H1.3? Um tempo muito longo aumenta o risco de um atacante sequestrar uma sessão deixada aberta em um computador público. Um tempo muito curto prejudica a usabilidade.]

??? "Métrica 2.1: Percentual de ações críticas registradas em logs"

    ### Evidências e Dados Brutos

    * **Método:** Análise de código fonte.
    * **Ações críticas definidas:** Login, exclusão de aluno, alteração de nota.
    * **Dados Coletados:**
        * Total de ações críticas analisadas: [PREENCHER]
        * Ações que geram entrada de log: [PREENCHER]
        * Cálculo: `([Com Log] / [Total]) * 100` = [VALOR FINAL]%

    ![Exemplo de ação crítica com log]
    ![Exemplo de ação crítica SEM log]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Excelente: ≥ 90%
        * Bom: 70% a 89%
        * Regular: 40% a 69%
        * Insatisfatório: < 40%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: O que isso significa? Se ações críticas não são logadas (invalidando H2.1), a rastreabilidade é impossível. Se um dado for alterado indevidamente, ninguém saberá quem fez ou quando fez. Isso impede qualquer auditoria.]

??? "Métrica 2.2: Percentual de logs com informações completas"

    ### Evidências e Dados Brutos

    * **Método:** Amostragem e análise dos registros de log.
    * **Informações completas:** (Usuário, Ação, Data/Hora).
    * **Dados Coletados:**
        * Total de logs (amostra): [PREENCHER]
        * Logs com informações completas: [PREENCHER]
        * Cálculo: `([Completos] / [Total]) * 100` = [VALOR FINAL]%

    ![Exemplo de arquivo de log do i-Educar]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL]%
    * **Critério (da Fase 2):**
        * Excelente: ≥ 80%
        * Bom: 60% a 79%
        * Regular: 40% a 59%
        * Insatisfatório: < 40%
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: Isso valida H2.2? Não adianta logar (M2.1) se o log é inútil. Um log que diz "Acesso Negado" sem dizer *quem* tentou acessar *o quê*, não serve para auditoria. Logs incompletos dificultam a resposta a incidentes.]

??? "Métrica 3.1: Número médio de testes de segurança por módulo principal"

    ### Evidências e Dados Brutos

    * **Método:** Inspeção do repositório de testes.
    * **Testes de segurança:** Testes que validam falhas de permissão, SQL Injection, XSS, etc.
    * **Dados Coletados:**
        * Nº de testes de segurança (Módulo Escola): [PREENCHER]
        * Nº de testes de segurança (Módulo Servidores): [PREENCHER]
        * Nº de testes de segurança (Módulo Educacenso): [PREENCHER]
        * Média: [VALOR FINAL]

    ![Exemplo de teste de segurança]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL] (média)
    * **Critério (da Fase 2):**
        * Excelente: ≥ 3
        * Bom: 2
        * Regular: 1
        * Insatisfatório: 0
    * **Classificação:** [PREENCHER: Excelente/Bom/Regular/Insatisfatório]

    ### Análise e Discussão

    [PREENCHER: Isso valida H3.1? A ausência (ou baixo número) de testes de segurança indica que a equipe de desenvolvimento não está ativamente prevenindo vulnerabilidades. A segurança do sistema depende apenas da "sorte" ou da revisão manual, o que é arriscado.]

??? "Métrica 3.2: Frequência média de atualização de dependências"

    ### Evidências e Dados Brutos

    * **Método:** Análise do histórico de commits do `composer.lock` ou `package-lock.json`.
    * **Dados Coletados:**
        * Data da última atualização de dependência: [PREENCHER DATA]
        * Data da penúltima atualização: [PREENCHER DATA]
        * Frequência média: [VALOR FINAL] meses

    ![Histórico de commits do composer.lock]

    ### Classificação da Métrica

    * **Resultado:** [VALOR FINAL] meses
    * **Critério (da Fase 2):**
        * Conforme: Atualização a cada ≤ 6 meses
        * Não conforme: Atualização > 6 meses
    * **Classificação:** [PREENCHER: Conforme/Não conforme]

    ### Análise e Discussão

    [PREENCHER: Isso valida H3.2 e H3.3? Dependências desatualizadas são a porta de entrada mais comum para ataques (ex: Log4Shell, etc.). Manter as dependências atualizadas é uma prática de desenvolvimento seguro essencial.]

---

## 4. Conclusão (Segurança)

[PREENCHER: Faça uma conclusão *específica* para a Segurança.
* Com base nos resultados das 7 métricas, o objetivo de Segurança foi atingido?
* Use os "Critérios para Julgamento" da Fase 2 (Aceitável, Parcialmente aceitável, Inaceitável) para dar um veredito sobre esta característica.
* Quais foram os principais pontos fortes e fracos encontrados? (Ex: "O sistema armazena senhas corretamente, mas falha gravemente no controle de acesso e no monitoramento de logs.")
* (Opcional) Quais hipóteses (H1.1, H1.2, H1.3, H2.1, H2.2, H3.1, H3.2, H3.3) foram validadas ou invalidadas pela coleta?]