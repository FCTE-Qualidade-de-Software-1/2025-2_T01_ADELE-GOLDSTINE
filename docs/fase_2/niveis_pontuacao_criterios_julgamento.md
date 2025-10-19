<!-- Observação da Manuella

pensei que esse próximo tópico poderia ser o mesmo para os 3 objetivos de medição, já que a gente vai usar os mesmos níveis de pontuação e critérios de julgamento para todos, então ele fica no final -->



## Níveis de Pontuação e Critérios de Julgamento

Para cada métrica definida por meio da abordagem GQM, foram estabelecidos níveis de pontuação que permitem interpretar os resultados de maneira padronizada, facilitando comparações e decisões. Esses níveis foram definidos com base em referências da literatura, benchmarks de ferramentas de análise estática e boas práticas de engenharia de software.

A seguir, apresenta-se a escala de pontuação definida pela equipe:

| Desempenho da Métrica | Pontuação | Interpretação Qualitativa |
| :--- | :---: | :--- |
| **Excelente** | 9 - 10 | Atende ou supera as expectativas de qualidade. Indica um código saudável e alinhado às boas práticas. |
| **Bom** | 7 - 8 | Atende de forma satisfatória, com pequenas e pontuais oportunidades de melhoria. |
| **Regular** | 4 - 6 | Apresenta deficiências perceptíveis que podem indicar débito técnico ou risco moderado. |
| **Insatisfatório** | 1 - 3 | Compromete significativamente a característica de qualidade, exigindo atenção e provável refatoração. |

<div align="center">
  <font size="4"><figcaption>Tabela 4: Níveis de pontuação e critérios de julgamento</figcaption></font>
</div>

### Critérios para Julgamento

Com base nas métricas e nos níveis de pontuação definidos, foram estabelecidos critérios de julgamento para interpretar os resultados da avaliação e apoiar a tomada de decisões. Os critérios são organizados por característica e baseiam-se na média de desempenho das métricas associadas a cada uma delas.

#### Critérios para Confiabilidade
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O sistema demonstra robustez e previsibilidade.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. O sistema funciona, mas pode apresentar instabilidades pontuais.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". A estabilidade do sistema é considerada crítica e propensa a falhas.

#### Critérios para Manutenibilidade
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O código é considerado claro, organizado e com baixo custo de manutenção.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. A manutenção é possível, mas com esforço considerável devido ao débito técnico.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". O código é de difícil compreensão e modificação, desestimulando novas contribuições.

#### Critérios para Segurança
* **Aceitável:** ≥ 70% das métricas classificadas como "Bom" ou "Excelente". O sistema adere às boas práticas de codificação segura.
* **Parcialmente aceitável:** Entre 40% e 69% das métricas com nível "Regular" ou superior. Foram identificadas vulnerabilidades de baixo ou médio risco.
* **Inaceitável:** > 30% das métricas atingindo o nível "Insatisfatório". Existem vulnerabilidades críticas que comprometem a integridade ou a confidencialidade dos dados.
