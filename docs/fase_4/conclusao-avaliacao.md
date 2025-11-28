# Conclusão da Fase 4 - Avaliação de Qualidade do i-Educar

Esta seção consolida os resultados da avaliação de qualidade do software [i-Educar](https://github.com/portabilis/i-educar), realizada através da execução do plano GQM (Goal-Question-Metric) estabelecido nas [fases anteriores](../fase_1/objeto-estudo.md). A avaliação focou em três características críticas de qualidade: **[Confiabilidade](./avaliacao-confiabilidade.md)**, **[Manutenibilidade](./avaliacao-manutenibilidade.md)** e **[Segurança](./avaliacao-seguranca.md)**.

## 1. Visão Geral da Avaliação

A [Fase 4](./introducao-avaliacao.md) representou a execução prática do processo de avaliação de qualidade, onde foram coletadas 17 métricas distribuídas entre as três características avaliadas:

- **[Confiabilidade](./avaliacao-confiabilidade.md):** 4 métricas (M1.1, M1.2, M2.1, M3.1)
- **[Manutenibilidade](./avaliacao-manutenibilidade.md):** 6 métricas (M1.1, M1.2, M2.1, M3.1, M3.2, M3.3)
- **[Segurança](./avaliacao-seguranca.md):** 7 métricas (M1.1, M1.2, M1.3, M2.1, M2.2, M3.1, M3.2)

Cada métrica foi coletada seguindo procedimentos rigorosos e rastreáveis, com evidências em vídeo, armazenamento estruturado na [planilha de coleta de dados](https://docs.google.com/spreadsheets/d/1xK9J1rp2x5ZSQL_L3FXkUHIDdK44DdboHlh9b1tmC_k/edit?usp=sharing) e análise crítica baseada nos critérios estabelecidos na [Fase 2](../fase_2/introducao_gqm.md).

---

## 2. Rastreabilidade das Avaliações

A tabela abaixo apresenta a rastreabilidade completa entre os objetivos GQM definidos na [Fase 2](../fase_2/introducao_gqm.md), questões, hipóteses, métricas e resultados obtidos:

### 2.1 Confiabilidade

*Detalhes completos na página de [Avaliação da Confiabilidade](./avaliacao-confiabilidade.md) | GQM definido na [Fase 2](../fase_2/gqm_confiabilidade.md)*

| Questão | Hipótese | Métrica | Resultado | Classificação | Status da Hipótese |
|---------|----------|---------|-----------|---------------|-------------------|
| **Q1: Qual é a estabilidade do código em relação à ocorrência de defeitos?** | H1.1: Densidade > 3 bugs/KLOC | M1.1: Densidade de Defeitos | 0,364 bugs/KLOC | Excelente | **Invalidada** |
| Q1 | H1.2: Commits de correção > 15% | M1.2: % Commits de Correção | 8,55% | Excelente | **Invalidada** |
| **Q2: Qual é o nível de robustez do código contra falhas em tempo de execução?** | H2.1: < 50% de operações I/O com try-catch | M2.1: Índice de Tratamento de Exceções | 20% | Insatisfatório | **Validada** |
| **Q3: Qual é a eficácia dos mecanismos de recuperação de dados?** | H3.1: Qualidade do backup < 5/10 | M3.1: Análise Qualitativa de Backup | 7/10 | Bom | **Invalidada** |

**Veredito:** Confiabilidade classificada como **ACEITÁVEL** (75% das métricas atingiram "Bom" ou "Excelente").

### 2.2 Manutenibilidade

*Detalhes completos na página de [Avaliação da Manutenibilidade](./avaliacao-manutenibilidade.md) | GQM definido na [Fase 2](../fase_2/gqm_manutenibilidade.md)*

| Questão | Hipótese | Métrica | Resultado | Classificação | Status da Hipótese |
|---------|----------|---------|-----------|---------------|-------------------|
| **Q1: Qual o impacto de realizar uma alteração no sistema?** | H1.1: Alto acoplamento e duplicação aumentam tempo de correção | M1.1: CBO | Média 18 / 1,70% classes insatisfatórias | Bom | **Parcialmente validada** |
| Q1 | H1.1 (continuação) | M1.2: Código Repetido | 7,4% | Insatisfatório | **Validada** |
| **Q2: Quão complexo é entender o código-fonte?** | H2.1: CC > 10 aumenta tempo de entendimento | M2.1: Complexidade Ciclomática | Média 1,62 / 0,67% métodos insatisfatórios | Bom | **Parcialmente validada** |
| **Q3: Como está a situação atual dos testes?** | H3.1: Cobertura < 70% aumenta bugs de regressão | M3.1: Cobertura de Teste | 31,2% | Insatisfatório | **Validada** |
| Q3 | H3.2: Tempo > 3s desestimula execução | M3.2: Densidade de Testes | 9,52 Testes/KLOC | Regular | N/A |
| Q3 | H3.2 (continuação) | M3.3: Tempo de Execução | 0,027s por teste | Bom | **Invalidada** |

**Veredito:** Manutenibilidade classificada como **PARCIALMENTE ACEITÁVEL** (50% das métricas atingiram "Bom" ou "Excelente", mas com problemas críticos em cobertura de testes e duplicação de código).

### 2.3 Segurança

*Detalhes completos na página de [Avaliação da Segurança](./avaliacao-seguranca.md) | GQM definido na [Fase 2](../fase_2/gqm_seguranca.md)*

| Questão | Hipótese | Métrica | Resultado | Classificação | Status da Hipótese |
|---------|----------|---------|-----------|---------------|-------------------|
| **Q1: Qual é o nível de robustez do controle de acesso?** | H1.1: Rotas críticas terão autorização | M1.1: % Rotas com Autorização | 15,46% | Insatisfatório | **Validada** |
| Q1 | H1.2: Senhas com hashing adequado | M1.2: Algoritmo de Hashing | Argon2 | Conforme | **Invalidada** |
| Q1 | H1.3: Sessões expiram em 60min | M1.3: Tempo de Expiração de Sessão | 120 min | Não conforme | **Validada** |
| **Q2: Qual é o nível de rastreabilidade das ações críticas?** | H2.1: ≥ 70% de ações críticas logadas | M2.1: % Ações Críticas Logadas | 20% | Insatisfatório | **Validada** |
| Q2 | H2.2: > 60% dos logs completos | M2.2: Qualidade dos Logs | 0% | Insatisfatório | **Validada** |
| **Q3: Em que medida o desenvolvimento segue práticas de segurança?** | H3.1: Densidade de testes ≤ 0,1 T/KLOC | M3.1: Testes de Segurança | 0,07 T/KLOC | Insatisfatório | **Validada** |
| Q3 | H3.2: Atualização de dependências > 6 meses | M3.2: Frequência de Atualização | 15 dias | Conforme | **Invalidada** |

**Veredito:** Segurança classificada como **INACEITÁVEL** (apenas 2 de 7 métricas foram conformes, com falhas críticas em controle de acesso, sessão e monitoramento).

---

## 3. Respostas às Questões do GQM

### 3.1 Confiabilidade

**Q1: Qual é a estabilidade do código em relação à ocorrência de defeitos?**

O i-Educar demonstra **excelente estabilidade e maturidade**. Com densidade de defeitos de 0,364 bugs/KLOC e apenas 8,55% de commits dedicados a correções, o sistema apresenta código robusto e estável, bem acima dos padrões da indústria. A maior parte do esforço de desenvolvimento está concentrada em novas funcionalidades, não em remediação de problemas.

**Q2: Qual é o nível de robustez do código contra falhas em tempo de execução?**

A robustez é o **ponto mais crítico da confiabilidade**. Apenas 20% das operações críticas de I/O possuem tratamento adequado de exceções. Embora o Laravel forneça abstrações com tratamento interno, o código legado e operações de shell não possuem proteção explícita contra falhas, representando risco operacional significativo.

**Q3: Qual é a eficácia dos mecanismos de recuperação de dados?**

Os mecanismos de backup apresentam **qualidade aceitável** (7/10), com código bem documentado, estruturado e seguindo boas práticas do Laravel. O principal ponto de atenção é a ausência de tratamento de erros nas operações de shell (`pg_restore`, `psql`), que pode resultar em falhas silenciosas durante a recuperação.

### 3.2 Manutenibilidade

**Q1: Qual o impacto de realizar uma alteração no sistema?**

O impacto é **moderado**, com aspectos positivos e negativos. O acoplamento geral é baixo (apenas 1,70% das classes têm CBO alto), facilitando alterações isoladas. Entretanto, a **alta duplicação de código (7,4%)** representa um problema sério, pois 2.485 blocos duplicados exigem manutenção redundante, aumentando o esforço e o risco de inconsistências.

**Q2: Quão complexo é entender o código-fonte do i-Educar?**

A complexidade geral é **baixa e bem controlada** (média de 1,62 de complexidade ciclomática por método). A maior parte do código é compreensível e segue estruturas simples. No entanto, existem **métodos pontuais extremamente complexos** (como `getExportFormatData` com CC=186) que representam desafios significativos de compreensão e manutenção.

**Q3: Como está a situação atual dos testes do i-Educar?**

A situação de testes apresenta um **paradoxo**: densidade regular (9,52 Testes/KLOC) com testes extremamente rápidos (0,027s por teste), mas **cobertura insuficiente (31,2%)**. Isso indica concentração de testes nos módulos modernos, com boa qualidade técnica, enquanto o código legado permanece sem proteção adequada. A baixa cobertura expõe mais de dois terços do sistema a riscos de regressão.

### 3.3 Segurança

**Q1: Qual é o nível de robustez do controle de acesso do sistema?**

O controle de acesso é **criticamente deficiente**, caracterizando Broken Access Control ([OWASP A01](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)). Apenas 15,46% das rotas críticas possuem regras de autorização, permitindo que usuários executem ações fora de seu perfil. A situação é agravada pelo tempo excessivo de expiração de sessão (120 minutos), que amplia a janela de exploração para ataques. O **único ponto forte** é o uso consistente de Argon2 para hashing de senhas.

**Q2: Qual é o nível de rastreabilidade das ações críticas?**

A rastreabilidade é **praticamente inexistente**. Apenas 20% das ações críticas são registradas em logs, e **nenhum log** contém os campos mínimos necessários (usuário, ação, data/hora). Isso caracteriza Insufficient Logging & Monitoring ([OWASP A09](https://owasp.org/Top10/A09_2021-Security_Logging_and_Monitoring_Failures/)), inviabilizando auditorias, investigações de incidentes e detecção de comportamentos suspeitos.

**Q3: Em que medida o desenvolvimento do sistema segue práticas de segurança?**

As práticas de segurança são **desiguais**. A densidade extremamente baixa de testes de segurança (0,07 T/KLOC) indica que vulnerabilidades comuns (XSS, SQL Injection, falhas de autorização) não são validadas automaticamente. Por outro lado, a **atualização frequente de dependências** (a cada 15 dias) é exemplar, mitigando riscos de componentes vulneráveis e demonstrando maturidade no gerenciamento de dependências.

---

## 4. Síntese dos Resultados

### 4.1 Panorama Geral por Característica

| Característica | Classificação Final | Métricas Boas/Excelentes | Métricas Insatisfatórias | Principal Ponto Forte | Principal Ponto Fraco |
|----------------|-------------------|------------------------|--------------------------|----------------------|----------------------|
| **Confiabilidade** | Aceitável | 3 de 4 (75%) | 1 (Tratamento de exceções) | Baixa densidade de defeitos (0,364 bugs/KLOC) | Apenas 20% de operações I/O com try-catch |
| **Manutenibilidade** | Parcialmente Aceitável | 3 de 6 (50%) | 2 (Cobertura e duplicação) | Complexidade controlada (CC média 1,62) | Cobertura de testes de 31,2% |
| **Segurança** | Inaceitável | 2 de 7 (29%) | 5 (Autorização, sessão, logs, testes) | Uso de Argon2 e atualização frequente de deps | 15,46% de rotas com autorização |

### 4.2 Padrões Identificados

**Dualidade Código Moderno vs. Legado:**

Todas as três características evidenciam a natureza híbrida do i-Educar. O código moderno (diretórios `/app` e `/src`) demonstra boas práticas, testes rápidos e estruturas bem projetadas, enquanto o código legado (`/ieducar`) carece de testes, possui duplicação elevada e não implementa mecanismos modernos de segurança e tratamento de erros.

**Pontos Fortes Consistentes:**

- Baixo acoplamento e complexidade ciclomática
- Densidade de defeitos excepcional
- Testes unitários rápidos e eficientes
- Atualização ágil de dependências
- Uso de hashing moderno (Argon2)

**Vulnerabilidades Críticas Recorrentes:**

- Ausência de tratamento de exceções em operações críticas
- Cobertura de testes concentrada e insuficiente
- Falta de mecanismos de autorização na maioria das rotas
- Ausência de logs de auditoria e monitoramento
- Alta duplicação de código

---

## 5. Validação das Hipóteses

Das 15 hipóteses formuladas na [Fase 2](../fase_2/introducao_gqm.md):

- **6 hipóteses foram validadas** (40%): H2.1 (Confiabilidade), H1.1-parte (Manutenibilidade), H3.1 (Manutenibilidade), H1.1, H1.3, H2.1, H2.2, H3.1 (Segurança)
- **6 hipóteses foram invalidadas** (40%): H1.1, H1.2, H3.1 (Confiabilidade), H3.2 (Manutenibilidade), H1.2, H3.2 (Segurança)
- **3 hipóteses foram parcialmente validadas** (20%): H1.1-acoplamento (Manutenibilidade), H2.1 (Manutenibilidade)

A taxa de 40% de invalidação das hipóteses iniciais demonstra que o processo GQM foi efetivo em revelar aspectos inesperados do sistema, contrariando suposições iniciais e fornecendo uma visão baseada em evidências.

---

## 6. Recomendações Prioritárias

Com base nos resultados consolidados, recomenda-se a priorização das seguintes ações:

### Prioridade Crítica (Segurança):

1. **Implementar controle de acesso em rotas críticas:** Revisar e adicionar middleware de autorização em todas as rotas POST, PUT, PATCH e DELETE.
2. **Reduzir tempo de expiração de sessão:** Alterar de 120 para 60 minutos (ou menos para operações sensíveis).
3. **Implementar sistema de logs de auditoria:** Registrar todas as ações críticas com usuário, ação, data/hora e resultado.

### Prioridade Alta (Confiabilidade e Manutenibilidade):

4. **Adicionar tratamento de exceções:** Mapear e proteger operações de I/O, especialmente no código legado e rotinas de backup.
5. **Expandir cobertura de testes:** Priorizar módulos críticos do código legado, focando em lógica de negócio essencial.
6. **Refatorar código duplicado:** Eliminar ou consolidar os 2.485 blocos de código duplicado identificados.

### Prioridade Média (Manutenibilidade):

7. **Criar testes de segurança automatizados:** Implementar validações de XSS, SQL Injection, autorização e sanitização de entrada.
8. **Revisar métodos de alta complexidade:** Refatorar métodos com CC > 100, priorizando `getExportFormatData` (CC=186).
9. **Documentar código legado crítico:** Adicionar documentação em módulos essenciais sem testes.

---

## 7. Conclusão Final

A avaliação de qualidade do i-Educar revelou um sistema com **fundação técnica sólida**, mas com **deficiências críticas em segurança e distribuição desigual de qualidade** entre código moderno e legado.

**Confiabilidade Aceitável:** O sistema é estável, com baixíssima densidade de defeitos e esforço de desenvolvimento focado em evolução. O principal risco é a baixa tolerância a falhas em operações críticas.

**Manutenibilidade Parcialmente Aceitável:** O código moderno é bem estruturado, com baixo acoplamento e complexidade controlada. Entretanto, a alta duplicação e a baixa cobertura de testes representam débito técnico significativo e risco de regressão.

**Segurança Inaceitável:** O sistema apresenta vulnerabilidades graves em controle de acesso, gestão de sessão e monitoramento, expondo dados sensíveis de menores de idade a riscos de exposição indevida. A situação é agravada pela ausência de testes de segurança automatizados.

**Veredito Geral:** O i-Educar requer ações **imediatas e prioritárias na camada de segurança** antes de ser considerado adequado para ambientes de produção que processam dados protegidos pela [LGPD](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm). As melhorias em confiabilidade e manutenibilidade, embora importantes, são menos urgentes que as correções de segurança.

A natureza [open-source do projeto](https://github.com/portabilis/i-educar) e a atividade regular de desenvolvimento (evidenciada pela atualização frequente de dependências) são fatores positivos que facilitam a implementação das recomendações propostas. Com as correções adequadas, especialmente em segurança, o i-Educar tem potencial para atingir níveis aceitáveis em todas as características avaliadas.

---

## Bibliografia

> [1] ISO/IEC 25010:2011. Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. International Organization for Standardization, 2011.

> [2] BRASIL. Lei nº 13.709, de 14 de agosto de 2018. Lei Geral de Proteção de Dados Pessoais (LGPD). Diário Oficial da União: seção 1, Brasília, DF, 15 ago. 2018.

> [3] OWASP Foundation. OWASP Top 10 – 2021: The Ten Most Critical Web Application Security Risks. 2021. Disponível em: https://owasp.org/www-project-top-ten/. Acesso em: 18 nov. 2025.

> [4] BASILI, Victor R.; CALDIERA, Gianluigi; ROMBACH, H. Dieter. The Goal Question Metric Approach. Encyclopedia of Software Engineering, v. 1, p. 528-532, 1994.

> [5] PORTÁBILIS. i-Educar: Software livre de gestão escolar. Versão 2.10.0. [S.l.]: Portábilis Tecnologia, 2025. Disponível em: https://github.com/portabilis/i-educar. Acesso em: 17 nov. 2025.

> [6] PRESSMAN, Roger S.; MAXIM, Bruce R. Software Engineering: A Practitioner's Approach. 9th ed. New York: McGraw-Hill Education, 2020.

> [7] SOMMERVILLE, Ian. Software Engineering. 10th ed. Boston: Pearson, 2016.

> [8] CHIDAMBER, Shyam R.; KEMERER, Chris F. A Metrics Suite for Object Oriented Design. IEEE Transactions on Software Engineering, v. 20, n. 6, p. 476-493, jun. 1994.

> [9] MARTIN, Robert C. Clean Code: A Handbook of Agile Software Craftsmanship. Upper Saddle River, NJ: Prentice Hall, 2008.

> [10] MCCABE, Thomas J. A Complexity Measure. IEEE Transactions on Software Engineering, v. SE-2, n. 4, p. 308-320, dez. 1976.


---

### Histórico de versão

| Versão |    Data    | Descrição                                                                                | Autor                                                  | Revisor                                            |
| :----: | :--------: | :--------------------------------------------------------------------------------------- | :----------------------------------------------------- | :------------------------------------------------- |
| `1.0`  | 11/11/2025 | Criação do documento e adição da formatação padrão seguida na fase                       | [Manuella Valadares](https://github.com/manuvaladares) | [Marcos Marinho](https://github.com/devMarcosVM)   |
| `1.1`  | 16/11/2025 | Adequação ao novo escopo de avaliação                                                    | [André Maia](http://github.com/andre-maia51)           |                                                    |
| `1.2`  | 17/11/2025 | Atualização da avaliação de segurança - Métricas 1.1, 1.3, 3.1 e 3.2                     | [Caio Antônio](http://github.com/Caio-Antonio)         | [Zenilda Vieira](https://github.com/ZenildaVieira) |
| `1.3`  | 17/11/2025 | Adição da coleta e análise das Métricas 1.1, 1.2 e 2.1 de Manutenibilidade | [André Maia](http://github.com/andre-maia51)       |   |
| `1.4`  | 19/11/2025 | Atualização da avaliação de segurança - Métricas 1.2, 2.1 e 2.2 e introdução e conclusão | [Zenilda Vieira](https://github.com/ZenildaVieira)     | [Caio Antônio](http://github.com/Caio-Antonio)     |
| `2.0`  | 28/11/2025 | Consolidação completa da Fase 4 com rastreabilidade GQM, respostas às questões e síntese dos resultados | [Manuella Valadares](https://github.com/manuvaladares) |  |
