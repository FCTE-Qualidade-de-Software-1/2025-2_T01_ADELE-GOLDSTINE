<!--  Observação da Manuella

AQUI IRIAM OS OUTROS OBJETIVOS DE MEDIÇÃO (MANUTENIBILIDADE E SEGURANÇA) COM SUAS RESPECTIVAS TABELAS, PERGUNTAS, HIPÓTESES, MÉTRICAS E DIAGRAMAS
 -->
 
## Objetivo de Medição 3 - Segurança


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
      <td>Segurança (confidencialidade, integridade e disponibilidade dos dados)</td>
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
    <font size="4"><figcaption>Tabela 3: Objetivo de Medição: Segurança</figcaption></font>
  </div>
</div>


---

### Perguntas e Hipóteses de Medição

**Questão 1: Mecanismos de Autenticação e Autorização**

>  O sistema i-Educar possui mecanismos eficazes de autenticação, autorização e controle de acesso?

* **Hipótese 1.1 (H1.1):** O sistema restringe adequadamente o acesso às funcionalidades de acordo com o perfil do usuário.  
* **Hipótese 1.2 (H1.2):** As senhas são armazenadas de com hashing e criptografia.  


**Questão 2: Monitoramento e Auditoria**

> O sistema i-Educar possui práticas e ferramentas eficazes de monitoramento e auditoria de segurança?

* **Hipótese 2.1 (H2.1):** As ações críticas dos usuários são registradas em logs de auditoria.  
* **Hipótese 2.2 (H2.2):** O sistema permite rastrear atividades suspeitas ou tentativas de acesso indevido.  
* **Hipótese 2.3 (H2.3):** Há mecanismos de alerta ou resposta automatizada a incidentes de segurança.  



**Questão 3: Desenvolvimento Seguro**

> O desenvolvimento do i-Educar segue práticas de desenvolvimento seguro e análise de vulnerabilidades?

* **Hipótese 3.1 (H3.1):** O código é periodicamente revisado para identificar vulnerabilidades conhecidas.  
* **Hipótese 3.2 (H3.2):** Há cobertura de testes automatizados voltados à segurança.  
* **Hipótese 3.3 (H3.3):** Ferramentas de análise estática são utilizadas durante o ciclo de desenvolvimento.  

---

### Seleção das Métricas

**Questão 1: Mecanismos de Autenticação e Autorização**

* **Métrica 1.1 – Presença de autenticação**  
    * **Definição:** Verificação se o sistema exige login para acessar páginas protegidas.  
    * **Coleta:** 
        a. Teste manual: tentar acessar URLs sem estar autenticado e verificar se o sistema redireciona para a tela de login.  
    * **Propósito:** Confirmar a existência de controle de autenticação básico.  

* **Métrica 1.2 – Existência de papéis/perfis de usuário**  
    * **Definição:** Quantidade de perfis de usuário com permissões distintas.  
    * **Coleta:** 
        a. Análise documental (ex: listagem de perfis no painel de administração ou código fonte).  
    * **Propósito:** Avaliar se há segregação de funções e autorização diferenciada.  



**Questão 2: Monitoramento e Auditoria**

* **Métrica 2.1 – Existência de logs de ações**  
    * **Definição:** Verificação se o sistema armazena logs de ações como login, exclusão, alteração.  
    * **Coleta:** 
        a. Análise com o grupo de mantenedores do sistema.  
    * **Propósito:** Identificar se há rastreabilidade mínima de eventos de segurança.  

* **Métrica 2.2 – Existência de registro de falhas de login**  
    * **Definição:** Verificação se tentativas de login incorretas são registradas.  
    * **Coleta:** 
        a. Tentar efetuar logins inválidos e verificar se o evento é exibido em logs ou relatórios.  
    * **Propósito:** Avaliar a capacidade de monitorar possíveis ataques de força bruta.  


**Questão 3: Desenvolvimento Seguro**

* **Métrica 3.1 – Presença de testes automatizados**  
    * **Definição:** Quantidade de testes automatizados existentes no projeto.  
    * **Coleta:** 
        a. Inspecionar repositório.  
    * **Propósito:** Confirmar práticas básicas de validação de código.  

* **Métrica 3.2 – Frequência de atualizações de dependências**  
    * **Definição:** Intervalo médio entre atualizações de dependências do projeto.  
    * **Coleta:** 
        a. Analisar histórico de commits e datas de atualização.  
    * **Propósito:** Avaliar se o projeto é mantido atualizado e protegido contra vulnerabilidades conhecidas.  

---

### Critérios de Julgamento para Segurança

* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O sistema adere às boas práticas de codificação segura.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. Foram identificadas vulnerabilidades de baixo ou médio risco.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". Existem vulnerabilidades críticas que comprometem a integridade ou a confidencialidade dos dados.

---

### Relação entre a Segurança, Perguntas e Métricas


<div align="center">
  <table border="1" cellspacing="0" cellpadding="8" style="border-collapse: collapse; text-align: left;">
    <tr>
      <th><b>Questão</b></th>
      <th><b>Métricas Simplificadas</b></th>
      <th><b>Tipo de Coleta</b></th>
    </tr>
    <tr>
      <td>1 – Autenticação e Autorização</td>
      <td>Presença de autenticação; Perfis de usuário</td>
      <td>Teste manual / Análise documental</td>
    </tr>
    <tr>
      <td>2 – Monitoramento e Auditoria</td>
      <td>Existência de logs; Registro de falhas de login</td>
      <td>Teste funcional / Observação</td>
    </tr>
    <tr>
      <td>3 – Desenvolvimento Seguro</td>
      <td>Presença de testes; Frequência de atualização de dependências</td>
      <td>Inspeção do repositório / Histórico de commits</td>
    </tr>
  </table>

  <div style="margin-top: 8px; text-align: center;">
    <font size="4"><figcaption>Tabela 4: Questões e Métricas Simplificadas</figcaption></font>
  </div>
</div>


<div align="center">
  <img src="https://github.com/FCTE-Qualidade-de-Software-1/2025-2_T01_ADELE-GOLDSTINE/blob/main/docs/assets/diagrama_seguranca.png" alt="Relação entre a Segurança, Perguntas e Métricas" style="max-width: 80%; height: auto; border-radius: 8px;">

  <div style="margin-top: 8px; text-align: center;">
    <font size="4"><figcaption>Figura 4: Diagrama GQM - Segurança. Autor: <a href="http://github.com/ZenildaVieira">Zenilda Vieira</figcaption></font>
  </div>
</div>

