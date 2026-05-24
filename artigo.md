# Simulação de Opinião Pública com LLMs: Um Estudo com Dados do Cesop

**Matheus Henrique de Oliveira Santos e Marina Cantarelli Barroca**  
Universidade Presbiteriana Mackenzie, São Paulo, SP, Brasil  
10409051@mackenzie.br; 10740412@mackenzie.br

---

## Resumo

Este trabalho apresenta uma abordagem de simulação de pesquisa de opinião pública usando um modelo de linguagem de grande escala (LLM). A partir do perfil sociodemográfico de respondentes reais da pesquisa 04839 do Cesop/Unicamp, o modelo Gemini 1.5 Flash simula respostas a questões sobre cotas universitárias e mudanças climáticas. As distribuições simuladas são comparadas com os dados reais de 2.000 respondentes, avaliando acurácia e aderência distribucional em três repetições independentes.

**Palavras-chave:** LLM, simulação de opinião pública, silicon sampling, desigualdade, Gemini.

---

## 1. Introdução

Pesquisas de opinião pública são instrumentos fundamentais para compreender percepções sociais. Argyle et al. propõem o conceito de *silicon sampling*: o uso de LLMs para simular respostas humanas a partir de perfis sociodemográficos, comparando os resultados com dados reais.

Este trabalho aplica essa abordagem aos dados da pesquisa **04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade** do Cesop/Unicamp (2023), investigando se o Gemini 1.5 Flash reproduz distribuições de resposta sobre cotas universitárias e mudanças climáticas.

---

## 2. Dados e Preparação

A pesquisa 04839 foi coletada em julho de 2023, com 2.000 respondentes em todo o Brasil. Após remoção de valores ausentes e respostas "Não respondeu", o dataset final contou com 1.849 respondentes.

As variáveis de perfil selecionadas foram: sexo, escolaridade (agrupada em 4 níveis), renda pessoal em salários mínimos e região geográfica.

As questões simuladas foram:

- **Q1 (P6B):** *"A maior presença de pessoas negras e indígenas nas universidades, por meio de cotas, é necessária para reduzir a desigualdade no Brasil"* — respostas agrupadas em Concorda / Neutro / Discorda
- **Q2 (P6E):** *"As mudanças climáticas e eventos extremos afetam mais as pessoas em situação de pobreza"* — Concorda / Neutro / Discorda

A amostra para simulação foi de 200 respondentes por rodada, com 3 repetições (seeds 42, 7 e 13).

---

## 3. Modelo LLM

Utilizou-se o **Gemini 1.5 Flash** via Google AI Studio (tier gratuito), por sua disponibilidade sem custo e capacidade de seguir instruções estruturadas em português. O modelo foi acessado via API Python (`google-generativeai`), sem fine-tuning ou ajuste de domínio.

---

## 4. Geração dos Prompts

Para cada respondente, foi construído um prompt descrevendo o perfil sociodemográfico completo, solicitando respostas no formato estruturado `Q1: [resposta] / Q2: [resposta]`. Apenas respostas pertencentes às opções válidas foram aceitas; demais foram descartadas como nulas.

---

## 5. Resultados

### 5.1 Acurácia por rodada

| Rodada | Seed | Acurácia Q1 | Acurácia Q2 |
|---|---|---|---|
| 1 | 42 | [valor] | [valor] |
| 2 | 7 | [valor] | [valor] |
| 3 | 13 | [valor] | [valor] |
| **Média** | | **[valor]** | **[valor]** |

### 5.2 Distribuições comparadas

[Inserir gráficos de barras real vs simulado para Q1 e Q2]

### 5.3 Acurácia por escolaridade e região

[Inserir gráficos de acurácia por grupo]

---

## 6. Conclusão

**[Preencher após análise dos resultados]**

---

## Referências

ARGYLE, L. P. et al. *Simulating Public Opinion: Comparing Distributional and Individual-Level Predictions from LLMs and Random Forests*. Disponível na pasta do professor.

CESOP/UNICAMP. *04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade*, 2023. Disponível em: https://www.cesop.unicamp.br. Acesso em: mai. 2026.

GOOGLE. *Gemini API Documentation*. Disponível em: https://ai.google.dev. Acesso em: mai. 2026.
