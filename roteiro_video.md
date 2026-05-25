# Roteiro de Fala — Vídeo do Projeto (máx. 6 min)

**Projeto:** Simulação de Opinião Pública com LLMs  
**Grupo:** Matheus Henrique de Oliveira Santos e Marina Cantarelli Barroca

---

## Slide 1 — Apresentação (0:00 – 0:45)

"Nesse trabalho a gente usou inteligência artificial pra simular respostas de uma pesquisa de opinião pública. A ideia vem de um artigo que propõe usar LLMs como 'silício sociológico': você dá o perfil de uma pessoa pro modelo, e ele tenta responder como essa pessoa responderia numa pesquisa real."

"A gente usou a pesquisa 04839 do Cesop, coletada em 2023 com 2.000 brasileiros sobre desigualdade, e testou dois modelos diferentes: o Gemini do Google e o Llama 3.3 da Meta."

---

## Slide 2 — A Pesquisa e as Questões (0:45 – 1:30)

"A gente escolheu duas questões. A primeira é sobre cotas nas universidades: 'A maior presença de pessoas negras e indígenas por meio de cotas é necessária para reduzir a desigualdade?' As opções eram Concorda, Neutro ou Discorda."

"A segunda é sobre mudanças climáticas: 'Eventos extremos afetam mais pessoas em situação de pobreza?' Mesmas opções."

"A escolha foi intencional: são questões onde escolaridade, renda e região tendem a influenciar bastante a resposta."

---

## Slide 3 — Preparação dos Dados e Otimização (1:30 – 2:15)

"Do dataset original com 2.000 respondentes, depois de remover valores ausentes, ficamos com 1.849 registros válidos."

"As variáveis de perfil foram sexo, escolaridade em quatro níveis, renda em salários mínimos e região."

"Pra otimizar o uso da API, em vez de fazer uma chamada por respondente, a gente mandou 20 perfis em cada chamada e pediu pro modelo responder tudo em JSON. Isso reduziu 200 chamadas pra 10 por rodada."

---

## Slide 4 — Modelos Testados (2:15 – 3:15)

"A gente começou com o Gemini 2.5 Flash Lite do Google, mas a quota do free tier estava em apenas 20 requisições por dia, abaixo do limite documentado de mil. Conseguimos rodar só 2 das 3 rodadas planejadas."

"Migramos pro Groq, que roda o Llama 3.3 de 70 bilhões de parâmetros. O free tier deles é muito mais generoso, 30 requisições por minuto sem limite diário restritivo. Com isso a gente conseguiu rodar as 3 rodadas completas."

"A mudança de código foi mínima: só substituir a biblioteca cliente e o formato da chamada da API."

---

## Slide 5 — Resultados Principais (3:15 – 5:00)

"Os resultados foram interessantes e contraintuitivos. À primeira vista, o Gemini parecia melhor: acurácia de 80% na Q1 contra 49% do Llama. Mas olhando a distribuição das respostas, a história muda completamente."

"O Gemini convergia quase totalmente pra opção majoritária. Na Q2 do clima, ele respondeu 100% Concorda. O Llama também colapsou, mas respondeu 95% Concorda. Ou seja, a acurácia alta do Gemini era um efeito do desbalanceamento, não capacidade real de simulação."

"Quebrando por escolaridade, encontramos o achado mais importante: Ensino Superior teve 83% de acurácia, Ensino Médio 62%, Ensino Fundamental 25% e Sem escolaridade 0%. Isso mostra um viés sociodemográfico claro: o modelo simula muito melhor perfis bem representados nos dados de treino."

"Por região, Norte teve só 27% de acurácia, o que reflete a sub-representação dessa região tanto no treino do modelo quanto na própria amostra da pesquisa."

---

## Slide 6 — Conclusão (5:00 – 6:00)

"As três principais conclusões são: primeiro, todos os LLMs testados têm viés de classe majoritária, dão a resposta mais comum quando a base é desbalanceada. Segundo, existe um viés sociodemográfico claro: o modelo simula muito pior perfis de baixa escolaridade e regiões menos representadas. Terceiro, métricas simples como acurácia podem enganar: o Gemini parecia melhor numericamente, mas o Llama foi qualitativamente mais útil por distribuir mais as respostas."

"Vale destacar também uma limitação prática: quotas dos free tiers de LLM variam muito e mudam sem aviso. A gente teve que migrar de Gemini pra Groq no meio do projeto. Pra trabalhos acadêmicos em escala, é importante ter flexibilidade."

"Como próximos passos, daria pra comparar com Random Forest, como o artigo de referência propõe, e usar métricas como F1 macro pra capturar melhor o desempenho em classes minoritárias."

"O código, os dados e o artigo estão no GitHub. Obrigado."

---

