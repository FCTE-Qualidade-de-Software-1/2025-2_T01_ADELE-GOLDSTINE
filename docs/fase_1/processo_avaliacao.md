# Fase 1 - Processo de Avaliação

## Aplicação escolhida 

---
## Classificação e Ênfase das Características de Qualidade

---
## Proposta de Avaliação e Melhoria

### 1. Objetivo
O objetivo desta proposta é estabelecer um processo de **avaliação contínua e sistemática** da qualidade do software i-Educar, identificando pontos fortes e aspectos a serem melhorados.  
A ideia é utilizar principalmente **métricas técnicas e ferramentas de análise automática**, resultando em uma avaliação mais ágil e menos dependente de disponibilidade externa.  


### 2. Dimensões de Qualidade Avaliadas
A partir das características apresentadas no documento do i-Educar e alinhadas à ISO/IEC 25010, foram selecionadas as seguintes dimensões prioritárias:  

#### 2.1 Confiabilidade
- O sistema deve assegurar disponibilidade estável e consistência no processamento de dados acadêmicos, evitando perda ou corrupção de registros de alunos, notas e matrículas.  

#### 2.2 Segurança
- Considerando que o software gerencia informações sensíveis de alunos, professores e instituições, é necessário garantir mecanismos de autenticação, autorização e proteção contra uso indevido.  

#### 2.3 Manutenibilidade
- Por ser software livre e colaborativo, a arquitetura do sistema deve permitir fácil atualização, evolução e correção de falhas, garantindo que comunidades locais possam adaptá-lo às suas necessidades.  

---

### 3. Estratégias de Avaliação
Para avaliar cada dimensão, serão utilizadas técnicas de medições automáticas:  

#### 3.1 Confiabilidade
- **Testes Automatizados**: ampliar cobertura de testes unitários e de integração em funcionalidades críticas (matrículas, notas, boletins).  
- **Monitoramento de Logs**: análise de registros de erros em produção para identificar falhas recorrentes.  

#### 3.2 Segurança
- **Varreduras Automáticas**: uso de ferramentas como *OWASP ZAP* para detecção de vulnerabilidades (injeção SQL, XSS, autenticação fraca).  
- **Revisões de Código**: aplicação de checklist de segurança em *pull requests*.  

#### 3.3 Manutenibilidade
- **Análise Estática de Código**: uso de *SonarQube* ou *CodeClimate* para identificar duplicação de código, complexidade ciclomática e code smells.  
- **Métricas de Código**: monitorar acoplamento entre módulos, tamanho de classes e funções, cobertura de testes nos módulos mais críticos.  
- **Revisões de Código**: padronizar *code reviews* com checklist de manutenibilidade (clareza de nomes, padrões de projeto, documentação mínima, tratamento de erros).  

---

### 4. Métricas de Qualidade
As métricas propostas permitem acompanhar a evolução do software em ciclos de melhoria contínua:  

#### 4.1 Confiabilidade
- **Cobertura de Testes (%)** – percentual de código protegido por testes automatizados.  
- **Taxa de Defeitos em Produção** – número de falhas registradas após cada release.  

#### 4.2 Segurança
- **Número de Vulnerabilidades Detectadas** – resultado de varreduras de segurança.  
- **Percentual de Issues de Segurança Resolvidas** – comparação entre vulnerabilidades abertas e corrigidas em cada ciclo.  

#### 4.3 Manutenibilidade
- **Duplicação de Código (%)** – índice gerado por análise estática.  
- **Número de “Code Smells” Reportados** – más práticas detectadas automaticamente.  
- **Cobertura de Testes nos Módulos Críticos (%)** – quanto maior, mais confiável a manutenção futura.  

---

### 5. Plano de Melhoria
Com base nas avaliações, propõem-se as seguintes ações de melhoria:  

1. **Confiabilidade**: propor a criação de novos testes automatizados e correção de falhas críticas.  
2. **Segurança**: propor a adoção de boas práticas do *OWASP Top 10* e reforço nos controles de acesso.  
3. **Manutenibilidade**: Incentivo ao uso de padrões de projeto e propostas de refatorações de módulos com alta complexidade e duplicados.  

---


## Especificação do Modelo


---
## ODS da ONU


---
## Referências

1. **BASILI, Victor R.; CALDIERA, Gianluigi; ROMBACH, H. Dieter.** The Goal Question Metric Approach. In: Encyclopedia of Software Engineering. New York: Wiley, 1994.

2. **CAMPIONE, Eric; SUBRAMANIAN, S.** SonarQube in Action. Manning Publications, 2013.

3. **FENTON, Norman E.; PFLEEGER, Shari Lawrence.** Software Metrics: A Rigorous and Practical Approach. 3. ed. Boca Raton: CRC Press, 2014.

4. **ISO.** ISO/IEC 12207:2017 – Systems and software engineering — Software life cycle processes. Geneva: International Organization for Standardization, 2017.

5. **ISO.** ISO/IEC 25010:2011 – Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. Geneva: International Organization for Standardization, 2011.

6. **OWASP FOUNDATION.** OWASP Top Ten. Disponível em: <https://owasp.org/www-project-top-ten/>. Acesso em: 28 set. 2025.

7. **PRESSMAN, Roger S.; MAXIM, Bruce R.** Engenharia de Software: uma abordagem profissional. 8. ed. Porto Alegre: McGraw Hill, 2016.

8. **SOMMERVILLE, Ian.** Engenharia de Software. 10. ed. São Paulo: Pearson, 2019.


---
## Histórico de versão

| Versão |    Data    | Descrição                                               | Autor                                                    | Revisor                                                  |
|:------:|:----------:|:--------------------------------------------------------|:---------------------------------------------------------|:---------------------------------------------------------|
| `1.0`  | 28/09/2025 |     Criação do documento e adição da sessão de "Proposta de Avaliação e Melhoria"   | [Carla Clementino](https://github.com/ccarlaa)      | [Caio Antônio](http://github.com/)            |
