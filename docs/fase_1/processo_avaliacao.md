# Fase 1 - Processo de Avaliação

## Aplicação escolhida 

> Lançando o maior software livre educacional do Brasil!

O **i-Educar** é um software livre de gestão escolar totalmente on-line que permite secretários escolares, professores, coordenadores e gestores da área possam utilizar uma ferramenta que produz informações e estatísticas em tempo real, com um banco de dados centralizado e de fácil acesso, diminuindo a necessidade de uso de papel, a duplicidade de documentos, o tempo de atendimento ao cidadão e racionalizando o trabalho do servidor público. Ele foi originalmente desenvolvido pela prefeitura de Itajaí - SC e disponibilizado no Portal do Software Público do Governo Federal em 2008, com o objetivo de atender às necessidades das Secretarias de Educação e Escolas Públicas de todo o Brasil.

**Vídeo:** [Conheça o i-Educar](https://www.youtube.com/watch?v=AHZn3vDDijQ)

### Tecnologias utilizadas

O projeto utiliza majoritariamente **PHP**, com o uso de bibliotecas como:
* [Laravel](https://laravel.com/)
* [PHPUnit](https://phpunit.de/)
* [PestPHP](https://pestphp.com/)
Além disso, também faz uso de algumas bibliotecas **JavaScript**, como o framework **Bootstrap**.

### Links úteis

* [Repositório no GitHub](https://github.com/portabilis/i-educar)
* [Fórum da Comunidade](https://forum.ieducar.org/)
* [Telegram da Comunidade](https://t.me/ieducar)
* [Guia de Contribuição](https://github.com/portabilis/i-educar/blob/2.9/CONTRIBUTING.md)
* [Guia de Instalação](https://github.com/portabilis/i-educar/blob/2.9/INSTALL.md)
* [Código de Conduta](https://github.com/portabilis/i-educar/blob/2.9/CODE-OF-CONDUCT.md)

---
## Classificação e Ênfase das Características de Qualidade
Para a avaliação do i-Educar, foram priorizadas três características de qualidade da ISO/IEC 25010: Confiabilidade, Segurança e Manutenibilidade. A escolha baseou-se no propósito do software e em seu papel estratégico no setor público, considerando que se trata de uma solução livre utilizada por secretarias e escolas para a gestão acadêmica e administrativa.

| Característica | Justificativa |
|:---------------|:-------------|
| **Confiabilidade** | O i-Educar armazena informações críticas (dados de alunos, matrículas, notas, relatórios escolares) que precisam estar disponíveis de forma estável e íntegra, sem falhas recorrentes que prejudiquem o funcionamento da rede escolar. |
| **Segurança** | Foi destacada em função do tratamento de dados sensíveis de alunos e professores, o que exige conformidade com boas práticas de proteção da informação, autenticação e autorização, prevenindo acessos indevidos. |
| **Manutenibilidade** | Foi priorizada por se tratar de um software livre e colaborativo, com evolução contínua pela comunidade. A capacidade de adaptação, correção e extensão do sistema é fundamental para garantir longevidade e adequação a diferentes contextos educacionais. |

Essa classificação reflete uma ênfase em características ligadas à continuidade de operação e confiança do usuário, de modo que a avaliação da qualidade tenha impacto prático na confiabilidade institucional do sistema, na proteção de dados pessoais e na sustentabilidade de sua evolução tecnológica.

Optou-se por não incluir características como desempenho, compatibilidade, funcionalidade e portabilidade, por não representarem riscos imediatos à qualidade percebida pelos usuários no contexto atual.

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


### 5. Plano de Melhoria
Com base nas avaliações, propõem-se as seguintes ações de melhoria:  

1. **Confiabilidade**: propor a criação de novos testes automatizados e correção de falhas críticas.  
2. **Segurança**: propor a adoção de boas práticas do *OWASP Top 10* e reforço nos controles de acesso.  
3. **Manutenibilidade**: Incentivo ao uso de padrões de projeto e propostas de refatorações de módulos com alta complexidade e duplicados.  

---


## Especificação do Modelo

O modelo de qualidade adotado para a avaliação do i-Educar baseia-se na norma **ISO/IEC 25010**, priorizando três características fundamentais no contexto do sistema: Confiabilidade, Segurança e Manutenibilidade. Essas dimensões, como citado acima, foram selecionadas por representarem aspectos críticos para o funcionamento contínuo, a proteção de dados sensíveis e a evolução da aplicação.

A abordagem metodológica seguirá os princípios do **GQM (Goal-Question-Metric)**, permitindo estruturar a avaliação por meio de objetivos claros, questões norteadoras e métricas específicas.

### Dimensões Avaliadas

#### 1. Confiabilidade
- **Objetivo:** Garantir a estabilidade e disponibilidade do sistema em ambientes escolares.  
- **Questões:** O sistema mantém operação contínua sem falhas críticas? A cobertura de testes é suficiente para prevenir regressões?  
- **Métricas:**  
  - Cobertura de testes automatizados.  
  - Tempo médio entre falhas.  

#### 2. Segurança
- **Objetivo:** Assegurar a proteção de dados sensíveis e a integridade das informações processadas pelo sistema.  
- **Questões:** Existem vulnerabilidades conhecidas no código? Os mecanismos de autenticação e autorização são robustos? O tempo de resposta a incidentes é adequado?  
- **Métricas:**  
  - Número de vulnerabilidades identificadas em auditorias.  
  - Tempo médio de resposta a incidentes de segurança.  

#### 3. Manutenibilidade
- **Objetivo:** Garantir que o software seja facilmente compreensível, modificável e evolutivo, permitindo contribuições da comunidade e adaptações futuras.  
- **Questões:** O código apresenta complexidade adequada? Existem partes críticas com excesso de duplicação? As refatorações são incorporadas continuamente?  
- **Métricas:**  
  - Percentual de duplicação de código.  
  - Número de code smells identificados por análise estática.  


---
## Objetivos de Desenvolvimento Sustentável da ONU

### 1. Objetivo

Aqui descrevemos os Objetivos de Desenvolvimento Sustentável com os quais o i-Educar se conecta, com metas/indicadores relevantes e justificativas de como o software pode contribuir para alcançá-los.

### 2. ODS e conexão com o *i-educar*

#### 2.1 ODS 4 — Educação de Qualidade  


<div style="display: table; border-collapse: collapse; width: auto; max-width: 40%;">
  <div style="display: table-row;">
    <div style="display: table-cell; vertical-align: top; padding: 10px; text-align: center;">
      <img src="../assets/ODS_4.png" alt="ODS 4" style="max-width: 100px; height: auto; border-radius: 8px;">
      <p><b>Figura 1:<br>ODS 4</b></p>
    </div>
    <div style="display: table-cell; vertical-align: top; padding: 10px;">
      <p><b>Descrição: </b> Assegurar educação inclusiva, equitativa e de qualidade, e promover oportunidades de aprendizagem ao longo da vida para todos. 
      [<a href="https://www.ipea.gov.br/ods/ods4.html">1</a>]</p>
    </div>
  </div>
</div>


**Metas relevantes (Brasil / IPEA):**  
- Meta 4.1: Até 2030, garantir que todas as meninas e meninos completem o ensino primário e secundário gratuito, equitativo e de qualidade, com resultados de aprendizagem eficazes.  
- Meta 4.3: Assegurar igualdade de acesso para todos os gêneros à educação técnica, profissional e superior de qualidade, a preços acessíveis, incluindo universidade.  
- Meta 4.4: Aumentar substancialmente o número de jovens e adultos com habilidades relevantes, inclusive competências técnicas e profissionais, para emprego, trabalho decente e empreendedorismo.  
- Meta 4.a: Construir e melhorar instalações físicas para educação, apropriadas para crianças, sensíveis às deficiências e ao gênero, e que proporcionem ambientes de aprendizagem seguros, inclusivos e eficazes.  

**Indicadores relacionados:**  
- Proporção de jovens de 15-17 anos matriculados no ensino médio.  
- Proficiência em leitura e matemática em diferentes fases do ensino fundamental.  
- Infraestrutura escolar (acessibilidade, segurança, salas e equipamentos).  

**Relação com o i-Educar:**  
- Fornece dados precisos sobre matrícula, frequência, conclusão e desempenho acadêmico, apoiando o monitoramento das metas 4.1 e 4.3.  
- Identifica desigualdades regionais e socioeconômicas, permitindo intervenções mais justas.  
- Apoia a gestão de recursos e relatórios que evidenciem deficiências de infraestrutura.  


#### 2.2 ODS 10 — Redução das Desigualdades 


<div style="display: table; border-collapse: collapse; width: auto; max-width: 40%;">
  <div style="display: table-row;">
    <div style="display: table-cell; vertical-align: top; padding: 10px; text-align: center;">
      <img src="../assets/ODS_10.png" alt="ODS 10" style="max-width: 100px; height: auto; border-radius: 8px;">
      <p><b>Figura 2:<br>ODS 10</b></p>
    </div>
    <div style="display: table-cell; vertical-align: top; padding: 10px;">
      <p><b>Descrição: </b>Reduzir a desigualdade dentro dos países e entre eles.  
      [<a href="https://www.ipea.gov.br/ods/ods10.html">2</a>]</p>
    </div>
  </div>
</div>

**Metas relevantes (Brasil / IPEA):**  
- Meta 10.1: Até 2030, sustentar o crescimento da renda dos 40% mais pobres a uma taxa maior que a média nacional.  
- Meta 10.2: Empoderar e promover inclusão social, econômica e política de todos, independentemente de idade, gênero, deficiência, raça, etnia ou condição econômica.  

**Indicadores relacionados:**  
- Taxa de crescimento da renda dos 40% mais pobres em comparação à média nacional.  
- Medidas de inclusão em acesso à educação, conectividade digital e recursos de gestão.  

**Relação com o i-Educar:**  
- Reduz desigualdades de acesso à informação e gestão entre redes escolares.  
- Identifica grupos vulneráveis (por localização, deficiência ou condição socioeconômica), apoiando políticas inclusivas.  
- Democratiza acesso à tecnologia por ser um sistema **open source**, sem custos de licenciamento.  


#### 2.3  ODS 16 — Paz, Justiça e Instituições Eficazes  

<div style="display: table; border-collapse: collapse; width: auto; max-width: 40%;">
  <div style="display: table-row;">
    <div style="display: table-cell; vertical-align: top; padding: 10px; text-align: center;">
      <img src="../assets/ODS_16.jpg" alt="ODS 16" style="max-width: 100px; height: auto; border-radius: 8px;">
      <p><b>Figura 3:<br>ODS 16</b></p>
    </div>
    <div style="display: table-cell; vertical-align: top; padding: 10px;">
      <p><b>Descrição: </b>Promover sociedades pacíficas e inclusivas, garantir acesso à justiça para todos e construir instituições eficazes, responsáveis e transparentes.  
      [<a href="https://www.ipea.gov.br/ods/ods16.html">3</a>]</p>
    </div>
  </div>
</div>
  

**Meta relevante (Brasil / IPEA):**  
- Meta 16.6: Desenvolver instituições eficazes, responsáveis e transparentes em todos os níveis.  

**Relação com o i-Educar:**  
- Mantém registros escolares auditáveis e confiáveis, fortalecendo a transparência.  
- Apoia a eficiência administrativa, reduz duplicidades e melhora o controle institucional.  
- Favorece a confiança pública ao disponibilizar informações de forma organizada e acessível.  



### 3. Conclusão 

O i-Educar demonstra alinhamento direto com os Objetivos de Desenvolvimento Sustentável, em especial os ODS 4, 10 e 16. Ao promover inclusão digital, organização e acesso à informação, o sistema contribui para uma educação de qualidade mais eficiente e transparente (ODS 4). Por ser uma solução open source, possibilita sua adoção em redes públicas de ensino sem custos de licenciamento, democratizando o acesso à tecnologia e reduzindo desigualdades (ODS 10). Além disso, fortalece a governança e a eficiência institucional no setor educacional, garantindo maior transparência e confiança nos processos de gestão (ODS 16). Essa integração reflete o princípio central da Agenda 2030 — *não deixar ninguém para trás* — ao favorecer a equidade por meio do monitoramento de desempenho escolar, a inclusão ao ampliar o acesso a ferramentas de gestão e a transparência ao assegurar registros auditáveis e acessíveis.

---

## Bibliografia

> **BASILI, Victor R.; CALDIERA, Gianluigi; ROMBACH, H. Dieter.** The Goal Question Metric Approach. In: Encyclopedia of Software Engineering. New York: Wiley, 1994.
>
> **CAMPIONE, Eric; SUBRAMANIAN, S.** SonarQube in Action. Manning Publications, 2013.
>
> **FENTON, Norman E.; PFLEEGER, Shari Lawrence.** Software Metrics: A Rigorous and Practical Approach. 3. ed. Boca Raton: CRC Press, 2014.
> 
> **ISO.** ISO/IEC 12207:2017 – Systems and software engineering — Software life cycle processes. Geneva: International Organization for Standardization, 2017.
> 
> **ISO.** ISO/IEC 25010:2011 – Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. Geneva: International Organization for Standardization, 2011.
> 
> **OWASP FOUNDATION.** OWASP Top Ten. Disponível em: <https://owasp.org/www-project-top-ten/>. Acesso em: 28 set. 2025.
> 
> **PRESSMAN, Roger S.; MAXIM, Bruce R.** Engenharia de Software: uma abordagem profissional. 8. ed. Porto Alegre: McGraw Hill, 2016.
> 
> **SOMMERVILLE, Ian.** Engenharia de Software. 10. ed. São Paulo: Pearson, 2019.
> 

## Referências Bibliográficas

> [1] Objetivo de Desenvolvimento Sustentável 4 - IPEA. Disponível em: <[ODS 4](https://www.ipea.gov.br/ods/ods4.html)>. Acessado em 28/09/2025.
> 
> [2] Objetivo de Desenvolvimento Sustentável 10 - IPEA. Disponível em: <[ODS 10](https://www.ipea.gov.br/ods/ods10.html)>. Acessado em 28/09/2025.
> 
> [3] Objetivo de Desenvolvimento Sustentável 16 - IPEA. Disponível em: <[ODS 16](https://www.ipea.gov.br/ods/ods16.html)>. Acessado em 28/09/2025.
> 
> 
---
## Histórico de versão

| Versão |    Data    | Descrição                                               | Autor                                                    | Revisor                                                  |
|:------:|:----------:|:--------------------------------------------------------|:---------------------------------------------------------|:---------------------------------------------------------|
| `1.0`  | 28/09/2025 |     Criação do documento e adição da sessão de "Proposta de Avaliação e Melhoria"   | [Carla Clementino](https://github.com/ccarlaa)      | [Caio Antônio](http://github.com/)            |
| `1.1`  | 28/09/2025 |     Adição da sessão de "Classificação e Ênfase das Características de Qualidade"   | [Marcos Marinho](https://github.com/devMarcosVM)| [Manuella Valadares](http://github.com/manuvaladares)            |
| `1.2`  | 28/09/2025 |     Adição da sessão de "Aplicação escolhida" com as informações do projeto   | [Manuella Valadares](https://github.com/manuvaladares)| [Marcos Marinho](https://github.com/devMarcosVM)            |
| `1.3`  | 28/09/2025 | Adição dos ODS, conexões e referências bibliográficas                         | [Zenilda Vieira](https://github.com/ZenildaVieira) | [André Maia](http://github.com/andre-maia51) |
