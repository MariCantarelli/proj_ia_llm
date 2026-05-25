# Simulação de Opinião Pública com LLMs: Um Estudo Comparativo com Dados do Cesop

**Matheus Henrique de Oliveira Santos; Marina Cantarelli Barroca**  
Universidade Presbiteriana Mackenzie, São Paulo, SP, Brasil  
10409051@mackenzie.br; 10740412@mackenzie.br

---

## Resumo

Este trabalho apresenta uma abordagem de simulação de pesquisa de opinião pública usando modelos de linguagem (LLMs). A partir do perfil sociodemográfico de respondentes reais da pesquisa Cesop 04839 sobre desigualdade no Brasil, os modelos Google Gemini 2.5 Flash Lite e Meta Llama 3.3 70B (via Groq) foram testados em rodadas independentes de 200 perfis. Devido a limitações de quota do free tier do Gemini, a execução completa do experimento foi feita com Llama. Os resultados mostram acurácia média de 49,33% na Q1 (cotas) e 63,83% na Q2 (clima), com forte viés de classe majoritária especialmente na Q2 (95% Concorda). A comparação parcial com Gemini sugere que esse modelo possui viés ainda mais extremo, inflacionando a acurácia pela convergência para a classe majoritária.

**Palavras-chave:** LLM, simulação de opinião pública, silicon sampling, desigualdade, Llama 3.3, Gemini.

---

## 1. Introdução

Pesquisas de opinião pública são instrumentos fundamentais para compreender percepções sociais. Argyle et al. propõem o conceito de *silicon sampling*: o uso de LLMs para simular respostas humanas a partir de perfis sociodemográficos, comparando os resultados com dados reais.

Este trabalho aplica essa abordagem aos dados da pesquisa **04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade** do Cesop/Unicamp (2023), investigando se modelos abertos reproduzem distribuições de resposta sobre cotas universitárias e mudanças climáticas.

---

## 2. Dados e Preparação

A pesquisa 04839 foi coletada em julho de 2023, com 2.000 respondentes em todo o Brasil. Após remoção de valores ausentes, o dataset final contou com 1.849 respondentes.

As variáveis de perfil selecionadas foram: sexo, escolaridade (agrupada em 4 níveis), renda pessoal em salários mínimos e região geográfica.

As questões simuladas foram:

- **Q1 (P6B):** *"A maior presença de pessoas negras e indígenas nas universidades, por meio de cotas, é necessária para reduzir a desigualdade no Brasil"* — Concorda / Neutro / Discorda
- **Q2 (P6E):** *"As mudanças climáticas e eventos extremos afetam mais as pessoas em situação de pobreza"* — Concorda / Neutro / Discorda

Para otimizar o uso da API, adotou-se uma estratégia de **envio em lotes**: 20 perfis por chamada, com resposta estruturada em JSON. Isso reduziu 200 chamadas por rodada para apenas 10.

---

## 3. Modelos LLM Testados

### 3.1 Tentativa inicial: Google Gemini 2.5 Flash Lite

A implementação inicial utilizou o modelo `gemini-2.5-flash-lite` da Google via API do AI Studio. Apesar da documentação oficial indicar quota de 1.000 requisições por dia no free tier, a quota efetivamente aplicada foi de apenas **20 requisições por dia**:

```
TooManyRequests: Quota exceeded for metric: 
generate_content_free_tier_requests, limit: 20
```

Conseguimos completar parcialmente 2 rodadas antes do esgotamento da quota diária. Os resultados parciais do Gemini foram usados como base de comparação.

### 3.2 Modelo final: Meta Llama 3.3 70B (via Groq)

O experimento foi finalizado com o modelo **Llama 3.3 70B Versatile** acessado via **Groq**, que oferece:

- Free tier robusto: 30 requisições por minuto
- ~14.400 requisições por dia
- Sem necessidade de cartão de crédito
- API compatível com padrão OpenAI

A migração exigiu mudanças mínimas no código (substituição da biblioteca cliente e do formato de chamada).

---

## 4. Geração dos Prompts

Cada prompt continha 20 perfis numerados e as duas perguntas, solicitando resposta em formato JSON. Exemplo:

```
1. Sexo:Feminino, 36a, Ensino Médio, Renda:Mais de 1 a 2 SM, Centro-Oeste
2. Sexo:Masculino, 67a, Ensino Fundamental, Renda:Mais de 1 a 2 SM, Centro-Oeste
...
```

O modelo respondia com um array JSON contendo as respostas Q1 e Q2 para cada perfil. Apenas respostas dentro das opções válidas eram contabilizadas; demais eram descartadas.

---

## 5. Resultados

### 5.1 Comparação entre os modelos testados

| Métrica | Gemini 2.5 Flash Lite (parcial) | Llama 3.3 70B (completo) |
|---|---|---|
| Rodadas concluídas | 2 de 3 (quota esgotada) | 3 de 3 |
| Acurácia média Q1 | 79,75% | **49,33%** |
| Acurácia média Q2 | 72,25% | **63,83%** |
| Distribuição Q2 simulado | 100% Concorda | 95% Concorda |
| Variância Q1 entre rodadas | 5,25 p.p. | 16,13 p.p. |
| Variância Q2 entre rodadas | 2,25 p.p. | 4,40 p.p. |

**Interpretação:** A acurácia mais alta do Gemini não significa melhor desempenho. O Gemini convergia quase totalmente para a classe majoritária (Concorda), inflando a métrica simples de acurácia em uma base desbalanceada. O Llama 3.3 distribuiu mais as respostas entre as três opções, acertando menos em termos numéricos, mas representando melhor a diversidade de opiniões.

### 5.2 Acurácia por rodada (Llama 3.3)

| Rodada | Seed | Acurácia Q1 | Acurácia Q2 |
|---|---|---|---|
| 1 | 42 | 57,00% | 70,00% |
| 2 | 7 | 49,00% | 61,50% |
| 3 | 13 | 42,00% | 60,00% |
| **Média** | | **49,33% (±6,13%)** | **63,83% (±4,40%)** |

A variância de 6,13 p.p. na Q1 entre rodadas indica que o modelo é relativamente instável: a mesma metodologia com sementes diferentes produz resultados consideravelmente distintos.

### 5.3 Distribuição Real vs Simulada (Llama 3.3)

**Q1 (Cotas):**
- Real: ~89% Concorda, ~5% Neutro, ~6% Discorda
- Simulado: ~62% Concorda, ~30% Neutro, ~8% Discorda

O modelo subestimou a aderência às cotas e superestimou as respostas neutras, sugerindo que ele "tempera" opiniões fortes.

**Q2 (Clima):**
- Real: ~75% Concorda, ~2% Neutro, ~23% Discorda
- Simulado: ~95% Concorda, ~3% Neutro, ~2% Discorda

Houve colapso quase total para Concorda na Q2. O modelo praticamente ignorou a opção Discorda, que representa quase um quarto das respostas reais.

### 5.4 Matriz de Confusão (Q1, Rodada 1)

| Real \ Simulado | Concorda | Neutro | Discorda |
|---|---|---|---|
| Concorda | 110 | 52 | 17 |
| Neutro | 6 | 4 | 0 |
| Discorda | 8 | 3 | 0 |

O modelo acertou 110 dos 179 Concorda (61%), mas zero acertos para Discorda. Confirma o padrão de classe majoritária com forte deslocamento para Neutro.

### 5.5 Acurácia por Escolaridade (Q1)

| Escolaridade | Acurácia |
|---|---|
| Ensino Superior | 83,61% |
| Ensino Médio | 62,34% |
| Ensino Fundamental | 25,00% |
| Sem escolaridade | 0,00% |

Esse é um dos achados mais importantes do trabalho: há uma **correlação clara entre escolaridade e acurácia**. O modelo simula muito melhor perfis de Ensino Superior do que de baixa escolaridade. Isso sugere que dados de treinamento dos LLMs contêm mais representações de perfis escolarizados, criando um viés sociodemográfico.

### 5.6 Acurácia por Região (Q1)

| Região | Acurácia |
|---|---|
| Centro-Oeste | 63,16% |
| Nordeste | 60,42% |
| Sudeste | 59,09% |
| Sul | 52,94% |
| Norte | 27,27% |

A região Norte teve acurácia muito baixa, possivelmente por dois fatores: baixa representação no dataset de treino dos LLMs e baixa amostra na pesquisa em si (poucos respondentes da região), o que torna a métrica instável.

---

## 6. Conclusão

O experimento mostra que LLMs open-weight conseguem capturar **tendências agregadas** da opinião pública brasileira, mas com limitações significativas:

1. **Viés de classe majoritária:** todos os modelos testados convergem para a resposta mais comum em questões desbalanceadas. Na Q2, tanto Gemini (100%) quanto Llama (95%) responderam quase exclusivamente Concorda, ignorando a opinião contrária expressiva (~23% nos dados reais).

2. **Viés sociodemográfico:** a acurácia varia drasticamente conforme o perfil simulado. Ensino Superior teve 83% de acurácia; Sem escolaridade, 0%. Isso indica que LLMs simulam melhor grupos super-representados em seus dados de treino.

3. **Trade-off honestidade vs acurácia:** o Llama 3.3 teve acurácia mais baixa que o Gemini, mas distribuiu melhor as respostas, sendo qualitativamente mais útil para análise sociológica. Acurácia simples mascara o comportamento do modelo em bases desbalanceadas.

4. **Variabilidade prática de provedores:** quotas dos free tiers variam entre provedores e mudam sem aviso. A migração forçada de Gemini para Groq durante o projeto mostra que aplicações acadêmicas de LLM precisam ter flexibilidade quanto à escolha de modelo.

Como próximos passos, seria interessante: (i) comparar com um Random Forest, conforme o artigo de Argyle et al.; (ii) usar métricas como F1 macro e divergência de Kullback-Leibler entre distribuições para avaliar melhor o desempenho em classes minoritárias; (iii) testar prompts com técnicas de *chain-of-thought* para reduzir o colapso na classe majoritária.

---

## Referências

ARGYLE, L. P. et al. *Simulating Public Opinion: Comparing Distributional and Individual-Level Predictions from LLMs and Random Forests*.

CESOP/UNICAMP. *04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade*, 2023. Disponível em: https://www.cesop.unicamp.br. Acesso em: mai. 2026.

GOOGLE. *Gemini API Documentation*. Disponível em: https://ai.google.dev. Acesso em: mai. 2026.

GROQ. *API Documentation*. Disponível em: https://console.groq.com/docs. Acesso em: mai. 2026.

META AI. *Llama 3.3 Model Card*. Disponível em: https://ai.meta.com/llama. Acesso em: mai. 2026.
