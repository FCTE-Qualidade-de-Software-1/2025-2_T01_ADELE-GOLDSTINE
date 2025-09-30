# Orientações da professora estão em itálico - APAGAR ANTES DA ENTREGA

***Há orientações gerais sobre a escrita e uso de IA na página inicial, por favor deêm uma lida!***

---

# Modelo de Qualidade
   
## Visão Geral do Modelo:

### Representação gráfica e descrição do modelo de qualidade
***Orientações da professora estão em itálico - APAGAR ANTES DA ENTREGA***
* *Objetivo: Executar a Fase 1 para definir os requisitos de avaliação da qualidade do software selecionado pela equipe, incluindo a Especificação inicial do modelo de qualidade*
* *Resultados esperados: Modelo de qualidade com descrição e representação gráfica*
* *Critério de avaliação 4 - Modelo de qualidade (adaptação + representação gráfica) - Escolha/adaptação do modelo de qualidade ao software ediagrama correspondente.*
    * *Existente e adequado; diagrama presente.*
    * *Não pode ter uso “de prateleira” sem justificar adaptações; o diagrama não pode ser confuso.* 
        * *Uso de prateleira => A equipe simplesmente usa um modelo pronto e tenta encaixá-lo na situação, sem explicar por que essa abordagem foi escolhida.*
    * *Adequado, com pequenas adaptações mencionadas; diagrama legível.*
    * *Excelente: adaptações justificadas por contexto e stakeholders; diagrama organizado, com ligações às métricas/itens priorizados.*

#### Especificação do Modelo

O modelo de qualidade adotado para a avaliação do i-Educar baseia-se na norma **ISO/IEC 25010**, priorizando três características fundamentais no contexto do sistema: Confiabilidade, Segurança e Manutenibilidade. Essas dimensões, como citado acima, foram selecionadas por representarem aspectos críticos para o funcionamento contínuo, a proteção de dados sensíveis e a evolução da aplicação.

A abordagem metodológica seguirá os princípios do **GQM (Goal-Question-Metric)**, permitindo estruturar a avaliação por meio de objetivos claros, questões norteadoras e métricas específicas.

#### Dimensões Avaliadas

##### Confiabilidade

* **Objetivo:** Garantir a estabilidade e disponibilidade do sistema em ambientes escolares.  
* **Questões:** O sistema mantém operação contínua sem falhas críticas? A cobertura de testes é suficiente para prevenir regressões?  
* **Métricas:**  
  * Cobertura de testes automatizados.  
  * Tempo médio entre falhas.  

##### Segurança

* **Objetivo:** Assegurar a proteção de dados sensíveis e a integridade das informações processadas pelo sistema.  
* **Questões:** Existem vulnerabilidades conhecidas no código? Os mecanismos de autenticação e autorização são robustos? O tempo de resposta a incidentes é adequado?  
* **Métricas:**  
  * Número de vulnerabilidades identificadas em auditorias.  
  * Tempo médio de resposta a incidentes de segurança.  

##### Manutenibilidade

* **Objetivo:** Garantir que o software seja facilmente compreensível, modificável e evolutivo, permitindo contribuições da comunidade e adaptações futuras.  
* **Questões:** O código apresenta complexidade adequada? Existem partes críticas com excesso de duplicação? As refatorações são incorporadas continuamente?  
* **Métricas:**  
  * Percentual de duplicação de código.  
  * Número de code smells identificados por análise estática.  


### Justificativa para a adaptação do modelo para o software em questão
***Orientações da professora estão em itálico - APAGAR ANTES DA ENTREGA***
* *Resultados esperados: A adaptação do modelo de qualidade deve refletir ausência/presença de componentes relevantes ao software avaliado.*
  
--- 

## Características de Qualidade:

### Características escolhidas
***Orientações da professora estão em itálico - APAGAR ANTES DA ENTREGA***
* *Seleção de características (SQuaRE): Escolher no mínimo 2 e no máximo 4 características de qualidade de produto, de forma que ao final do projeto seja apresentada a relação entre elas a partir dos resultados obtidos com a execução da avaliação.*
* *A característica Usabilidade não pode ser escolhida.*
* *Resultados esperados: Lista das características escolhidas (exceto usabilidade), com os critérios de priorização adotados e sua aplicação*
* *Apresenta os critérios de priorização adotados.*
* *Critériode avaliação 5 - Seleção e priorização de características - Escolhe 2–4 características exceto usabilidade e justifica a priorização.*
    * *Seleção não pode ser frágil; não pode haver priorização implícita ou subjetiva; não pode incluir usabilidade*
    * *Seleção adequada; priorização não pode ser básica e não pode ser pouco conectada ao propósito.*
    * *Seleção coerente; priorização justificada por critérios (ex.: risco, impacto, esforço) e por stakeholders.*
    * *Priorização robusta, com método explícito (ex.: matriz impacto×risco, MoSCoW com pesos) e trade-offs discutidos.*

#### Classificação e Ênfase das Características de Qualidade

Para a avaliação do i-Educar, foram priorizadas três características de qualidade da ISO/IEC 25010: Confiabilidade, Segurança e Manutenibilidade. A escolha baseou-se no propósito do software e em seu papel estratégico no setor público, considerando que se trata de uma solução livre utilizada por secretarias e escolas para a gestão acadêmica e administrativa.

| Característica | Justificativa |
|:---------------|:-------------|
| **Confiabilidade** | O i-Educar armazena informações críticas (dados de alunos, matrículas, notas, relatórios escolares) que precisam estar disponíveis de forma estável e íntegra, sem falhas recorrentes que prejudiquem o funcionamento da rede escolar. |
| **Segurança** | Foi destacada em função do tratamento de dados sensíveis de alunos e professores, o que exige conformidade com boas práticas de proteção da informação, autenticação e autorização, prevenindo acessos indevidos. |
| **Manutenibilidade** | Foi priorizada por se tratar de um software livre e colaborativo, com evolução contínua pela comunidade. A capacidade de adaptação, correção e extensão do sistema é fundamental para garantir longevidade e adequação a diferentes contextos educacionais. |

Essa classificação reflete uma ênfase em características ligadas à continuidade de operação e confiança do usuário, de modo que a avaliação da qualidade tenha impacto prático na confiabilidade institucional do sistema, na proteção de dados pessoais e na sustentabilidade de sua evolução tecnológica.

Optou-se por não incluir características como desempenho, compatibilidade, funcionalidade e portabilidade, por não representarem riscos imediatos à qualidade percebida pelos usuários no contexto atual.


### Relação das características com o propósito da avaliação
***Orientações da professora estão em itálico - APAGAR ANTES DA ENTREGA***
* *Resultados esperados: O propósito e o tipo de produto devem orientar a seleção das características e o escopo.*
* *Resultados esperados: Relação das características de qualidade priorizadas com o propósito declarado.*

---