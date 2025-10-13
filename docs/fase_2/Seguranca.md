<!--  Observação da Manuella

AQUI IRIAM OS OUTROS OBJETIVOS DE MEDIÇÃO (MANUTENIBILIDADE E SEGURANÇA) COM SUAS RESPECTIVAS TABELAS, PERGUNTAS, HIPÓTESES, MÉTRICAS E DIAGRAMAS
 -->
 
## Objetivo de Medição 3 - Segurança


O objetivo principal da análise da característica Segurança do sistema i-Educar é assegurar a proteção eficaz dos dados pessoais e institucionais que são continuamente processados e armazenados pelo sistema, especialmente considerando sua implementação em redes públicas de ensino, onde a integridade, confidencialidade e disponibilidade da informação são imperativas. Essa avaliação visa identificar e quantificar aspectos vitais que possam afetar a confiança dos usuários e a conformidade com a Lei Geral de Proteção de Dados (LGPD), além de garantir que vulnerabilidades técnicas sejam mitigadas pela comunidade de desenvolvedores e mantenedores open-source.

Utilizando o modelo Goal Question Metric (GQM), essa análise traduz a preocupação abstrata com a segurança em metas mensuráveis, por meio das seguintes diretrizes:

- Verificar e medir a robustez dos mecanismos de autenticação, autorização e controle de acesso para evitar acessos indevidos e garantir que apenas usuários autorizados possam manipular dados sensíveis ou realizar operações críticas no sistema.
- Avaliar a presença e eficiência das estratégias de auditoria e monitoramento de eventos de segurança, que promovem a detecção precoce de tentativas de invasão, falhas ou irregularidades, habilitando respostas rápidas e mitigação de danos.
- Medir as práticas de desenvolvimento seguro adotadas, através da avaliação da cobertura e qualidade dos testes automatizados específicos para segurança, revisões de código focalizadas em vulnerabilidades conhecidas e utilização de ferramentas para análise estática do código.
- Determinar o impacto potencial de falhas de segurança por meio de avaliações quantitativas e qualitativas que considerem a severidade das consequências, o risco de exposição dos dados e a probabilidade de ocorrência das falhas.
- Fornecer recomendações estratégicas e tecnicamente fundamentadas para fortalecer a segurança do sistema, garantindo sua sustentabilidade e a confiança contínua dos usuários e órgãos públicos que o utilizam.

Esta análise contextualiza a segurança não apenas como um requisito técnico, mas como um fator crítico para a manutenção da confiança institucional e para a observância dos direitos dos cidadãos. Sendo um software que impacta diretamente o setor educacional público, a segurança do i-Educar deve ser monitorada e aprimorada continuamente, assegurando que o sistema cumpra seu papel de forma responsável, confiável e transparente.


**Tabela 3** - Objetivo de Medição 3: Segurança.

| **Analisar**             | o i-Educar                                                                                                        |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| **Para o propósito de**  | Garantir a proteção das informações pessoais e institucionais contra acessos indevidos, vulnerabilidades e falhas |
| **Com respeito a**       | Segurança (confidencialidade, integridade e disponibilidade dos dados)                                            |
| **Do ponto de vista da** | Comunidade de desenvolvedores e mantenedores open-source do i-Educar                                              |
| **No contexto da**       | Disciplina de Qualidade de Software (FCTE - UnB) e ambiente de sistemas públicos de ensino                        |

---


### Perguntas e Hipóteses de Medição

**Questão 1: O sistema i-Educar possui mecanismos eficazes de autenticação, autorização e controle de acesso?**

* **Hipótese 1.1 (H1.1):** O sistema restringe adequadamente o acesso às funcionalidades de acordo com o perfil do usuário.  
* **Hipótese 1.2 (H1.2):** As senhas são armazenadas de com hashing e criptografia.  

---

**Questão 2: O sistema i-Educar possui práticas e ferramentas eficazes de monitoramento e auditoria de segurança?**

* **Hipótese 2.1 (H2.1):** As ações críticas dos usuários são registradas em logs de auditoria.  
* **Hipótese 2.2 (H2.2):** O sistema permite rastrear atividades suspeitas ou tentativas de acesso indevido.  
* **Hipótese 2.3 (H2.3):** Há mecanismos de alerta ou resposta automatizada a incidentes de segurança.  

---

**Questão 3: O desenvolvimento do i-Educar segue práticas de desenvolvimento seguro e análise de vulnerabilidades?**

* **Hipótese 3.1 (H3.1):** O código é periodicamente revisado para identificar vulnerabilidades conhecidas.  
* **Hipótese 3.2 (H3.2):** Há cobertura de testes automatizados voltados à segurança.  
* **Hipótese 3.3 (H3.3):** Ferramentas de análise estática são utilizadas durante o ciclo de desenvolvimento.  

---

### Seleção das Métricas

**Questão 1: Mecanismos de Autenticação e Autorização**

* **Métrica 1.1 – Presença de autenticação**  
    * **Definição:** Verificação se o sistema exige login para acessar páginas protegidas.  
    * **Coleta:** Teste manual: tentar acessar URLs sem estar autenticado e verificar se o sistema redireciona para a tela de login.  
    * **Propósito:** Confirmar a existência de controle de autenticação básico.  

* **Métrica 1.2 – Existência de papéis/perfis de usuário**  
    * **Definição:** Quantidade de perfis de usuário com permissões distintas.  
    * **Coleta:** Análise documental (ex: listagem de perfis no painel de administração ou código fonte).  
    * **Propósito:** Avaliar se há segregação de funções e autorização diferenciada.  

---

**Questão 2: Monitoramento e Auditoria**

* **Métrica 2.1 – Existência de logs de ações**  
    * **Definição:** Verificação se o sistema armazena logs de ações como login, exclusão, alteração.  
    * **Coleta:** Annálise com o grupo de mantenedores do sistema.  
    * **Propósito:** Identificar se há rastreabilidade mínima de eventos de segurança.  

* **Métrica 2.2 – Existência de registro de falhas de login**  
    * **Definição:** Verificação se tentativas de login incorretas são registradas.  
    * **Coleta:** Tentar efetuar logins inválidos e verificar se o evento é exibido em logs ou relatórios.  
    * **Propósito:** Avaliar a capacidade de monitorar possíveis ataques de força bruta.  

---

**Questão 3: Desenvolvimento Seguro**

* **Métrica 3.1 – Presença de testes automatizados**  
    * **Definição:** Quantidade de testes automatizados existentes no projeto.  
    * **Coleta:** Inspecionar repositório.  
    * **Propósito:** Confirmar práticas básicas de validação de código.  

* **Métrica 3.2 – Frequência de atualizações de dependências**  
    * **Definição:** Intervalo médio entre atualizações de dependências do projeto.  
    * **Coleta:** Analisar histórico de commits e datas de atualização.  
    * **Propósito:** Avaliar se o projeto é mantido atualizado e protegido contra vulnerabilidades conhecidas.  

---

### Relação entre a Segurança, Perguntas e Métricas

| **Questão** | **Métricas Simplificadas** | **Tipo de Coleta** |
| ------------ | --------------------------- | ------------------ |
| 1 – Autenticação e Autorização | Presença de autenticação; Perfis de usuário | Teste manual / Análise documental |
| 2 – Monitoramento e Auditoria | Existência de logs; Registro de falhas de login | Teste funcional / Observação |
| 3 – Desenvolvimento Seguro | Presença de testes; Frequência de atualização de dependências | Inspeção do repositório / Histórico de commits |


![Relação entre a Segurança, Perguntas e Métricas](../assets/diagrama_seguranca.png)

<p align="center"><b>Figura 3</b> - Diagrama ilustrando a relação entre a característica de Segurança, as perguntas formuladas e as métricas definidas na abordagem GQM.</p>

