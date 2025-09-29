# Especificação do Modelo

O modelo de qualidade adotado para a avaliação do i-Educar baseia-se na norma **ISO/IEC 25010**, priorizando três características fundamentais no contexto do sistema: Confiabilidade, Segurança e Manutenibilidade. Essas dimensões, como citado acima, foram selecionadas por representarem aspectos críticos para o funcionamento contínuo, a proteção de dados sensíveis e a evolução da aplicação.

A abordagem metodológica seguirá os princípios do **GQM (Goal-Question-Metric)**, permitindo estruturar a avaliação por meio de objetivos claros, questões norteadoras e métricas específicas.

## Dimensões Avaliadas

### 1. Confiabilidade

* **Objetivo:** Garantir a estabilidade e disponibilidade do sistema em ambientes escolares.  
* **Questões:** O sistema mantém operação contínua sem falhas críticas? A cobertura de testes é suficiente para prevenir regressões?  
* **Métricas:**  
  * Cobertura de testes automatizados.  
  * Tempo médio entre falhas.  

### 2. Segurança

* **Objetivo:** Assegurar a proteção de dados sensíveis e a integridade das informações processadas pelo sistema.  
* **Questões:** Existem vulnerabilidades conhecidas no código? Os mecanismos de autenticação e autorização são robustos? O tempo de resposta a incidentes é adequado?  
* **Métricas:**  
  * Número de vulnerabilidades identificadas em auditorias.  
  * Tempo médio de resposta a incidentes de segurança.  

### 3. Manutenibilidade

* **Objetivo:** Garantir que o software seja facilmente compreensível, modificável e evolutivo, permitindo contribuições da comunidade e adaptações futuras.  
* **Questões:** O código apresenta complexidade adequada? Existem partes críticas com excesso de duplicação? As refatorações são incorporadas continuamente?  
* **Métricas:**  
  * Percentual de duplicação de código.  
  * Número de code smells identificados por análise estática.  
