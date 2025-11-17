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

???+ "M1.1: Percentual de rotas críticas com regras de autorização"

    ### Evidências e Dados Brutos

    * **Método:** Revisão de código fonte (ex: arquivos de rota, controllers).
    * **Rotas críticas analisadas:** 1. POST /matricula/{...}/enturmar/{...}
       * Permissão: modify:enrollment (Enturmar matrícula)
   2. POST /matricula/{...}/remanejar/{...}
       * Permissão: modify:relocate (Remanejar matrícula)
   3. POST /atualiza-situacao-matriculas
       * Permissão: modify:update_registration_status (Atualizar situação de matrículas)
   4. POST /exportacoes/exportar
       * Permissão: modify:data_export (Exportação de dados)
   5. POST /arquivo/exportacoes/novo
       * Permissão: modify:document_export (Exportação de documentos)
   6. POST /avisos/publicacao/criar
       * Permissão: create:announcement (Criar avisos)
   7. POST /avisos/publicacao/{...}/editar
       * Permissão: modify:announcement (Editar avisos)
   8. POST /importacao-situacao-final/upload
       * Permissão: modify:final_status_import (Importar situação final)
   9. POST /importacao-situacao-final/importar
       * Permissão: modify:final_status_import (Importar situação final)
   10. POST /atualiza-data-entrada
       * Permissão: modify:update_registration_date (Atualizar data de entrada)
   11. POST /atualiza-etapa
       * Permissão: modify:stage (Atualizar etapa)
   12. POST /ano-letivo-em-lote/processar
       * Permissão: modify:academic_year_import (Importar ano letivo em lote)
   13. POST /atualizacao-em-lote-series-escola/processo
       * Permissão: modify:school_grade (Atualizar séries da escola em lote)
   14. POST /bloquear-enturmacao
       * Permissão: modify:block_enrollment (Bloquear enturmação)
   15. POST /dispensa-lote
       * Permissão: modify:batch_exemption (Dispensar em lote)

    * **Dados Coletados:**
        * Total de rotas críticas: 97
        * Rotas com checagem de autorização: 15
        * Cálculo: `([Com Autorização] / [Total]) * 100` = 15,46%

    ![Imagem 1](../assets/evidencias_seguranca/print_1.png)
    Linhas 45 e 48
    ![Imagem 2](../assets/evidencias_seguranca/print_2.png)
    Linha 119
    ![Imagem 3](../assets/evidencias_seguranca/print_3.png)
    Linhas 134 e 138
    ![Imagem 4](../assets/evidencias_seguranca/print_4.png)
    Linhas: 142, 144, 149, 152, 156, 159, 162, 167, 171
    ![Imagem 5](../assets/evidencias_seguranca/print_5.png)
    Linha 189

    ### Classificação da Métrica

    * **Resultado:** 15,46%
    * **Critério (da Fase 2):**
        * Excelente: ≥ 90%
        * Bom: 70% a 89%
        * Regular: 40% a 69%
        * Insatisfatório: < 40%
    * **Classificação:** Insatisfatório

    ### Análise e Discussão

    [PREENCHER: O que esse percentual indica? Um valor baixo é uma falha crítica de segurança (Broken Access Control). Significa que um usuário com permissão baixa (ex: professor) poderia acessar dados de outro nível (ex: administrador). Isso valida H1.1?]

??? "M1.2: Método de armazenamento de senhas"

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

??? "M1.3: Tempo médio de expiração da sessão"

    ### Evidências e Dados Brutos

    * **Método:** Análise do arquivo session.php.
    * **Parâmetro analisado:** `SESSION_LIFETIME`.
    * **Dado Coletado:** Tempo de expiração configurado: 120 minutos.

    ![Arquivo de configuração da sessão](../assets/evidencias_seguranca/session.png)

    ### Classificação da Métrica

    * **Resultado:** 120 minutos
    * **Critério (da Fase 2):**
        * Conforme: Menor ou igual a 60
        * Não conforme: Acima de 60
    * **Classificação:** Não conforme

    ### Análise e Discussão

    [PREENCHER: Isso valida a H1.3? Um tempo muito longo aumenta o risco de um atacante sequestrar uma sessão deixada aberta em um computador público. Um tempo muito curto prejudica a usabilidade.]

??? "M2.1: Percentual de ações críticas registradas em logs"

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

??? "M2.2: Percentual de logs com informações completas"

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

??? "M3.1: Densidade de testes de segurança (Testes/KLOC)"

    ### Evidências e Dados Brutos

    * **Método:** Uso de IA para identificar testes de segurança e `cloc`.
    * **Testes de segurança:** Testes que validam falhas de permissão, SQL Injection, XSS, etc.
    * **Dados Coletados:**
        * Nº total de testes de segurança: 25
        * KLOC total do código de produção: 341
        * Cálculo: `(Nº Testes de Segurança / (KLOC Total / 1000))` = 0,07 Testes/KLOC

    ![Medição do KLOC](../assets/evidencias_seguranca/cloc.png)
    ![Busca dos testes](../assets/evidencias_seguranca/contagem.png)

    ### Classificação da Métrica

    * **Resultado:** 0,07 Testes/KLOC
    * **Critério (da Fase 2):**
        * Excelente: > 1
        * Bom: > 0.5
        * Regular: > 0.1
        * Insatisfatório: ≤ 0.1
    * **Classificação:** Insatisfatório

    ### Análise e Discussão

    [PREENCHER: Isso valida H3.1? A ausência (ou baixo número) de testes de segurança indica que a equipe de desenvolvimento não está ativamente prevenindo vulnerabilidades. A segurança do sistema depende apenas da "sorte" ou da revisão manual, o que é arriscado.]

??? "M3.2: Frequência média de atualização de dependências"

    ### Evidências e Dados Brutos

    * **Método:** Análise do histórico de commits no Github`.
    * **Descoberta:** O sistema possui um mecanismo de atualização automática das dependências, portanto possui atualizações praticamente todos os meses.
    * **Dados Coletados:**
        * Data da última atualização de dependência: 12/11/2025
        * Data da penúltima atualização: 21/10/2025
        * Frequência média: a cada nova atualização disponível

    ![Histórico de commits](../assets/evidencias_seguranca/commits.png)

    ### Classificação da Métrica

    * **Resultado:** a cada 15 dias
    * **Critério (da Fase 2):**
        * Conforme: Atualização a cada ≤ 6 meses
        * Não conforme: Atualização > 6 meses
    * **Classificação:** Conforme

    ### Análise e Discussão

    [PREENCHER: Isso valida H3.2? Dependências desatualizadas são a porta de entrada mais comum para ataques (ex: Log4Shell, etc.). Manter as dependências atualizadas é uma prática de desenvolvimento seguro essencial.]

---

## 4. Conclusão (Segurança)

[PREENCHER: Faça uma conclusão *específica* para a Segurança.
* Com base nos resultados das 7 métricas, o objetivo de Segurança foi atingido?
* Use os "Critérios para Julgamento" da Fase 2 (Aceitável, Parcialmente aceitável, Inaceitável) para dar um veredito sobre esta característica.
* Quais foram os principais pontos fortes e fracos encontrados? (Ex: "O sistema armazena senhas corretamente, mas falha gravemente no controle de acesso e no monitoramento de logs.")
* (Opcional) Quais hipóteses (H1.1, H1.2, H1.3, H2.1, H2.2, H3.1, H3.2) foram validadas ou invalidadas pela coleta?]