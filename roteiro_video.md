# Roteiro de Fala — Vídeo do Projeto (máx. 6 min)

**Projeto:** Simulação de Opinião Pública com LLMs  
**Grupo:** Matheus Henrique de Oliveira Santos e Marina Cantarelli Barroca  
**Referência de tempo por slide:** ~1 min cada

---

## Slide 1 — Apresentação do Projeto (0:00 – 0:45)

> "Nesse trabalho a gente usou inteligência artificial pra simular respostas de uma pesquisa de opinião pública. A ideia vem de um artigo que propõe usar LLMs como o que ele chama de 'silício sociológico': você dá o perfil de uma pessoa pro modelo, e ele tenta responder como essa pessoa responderia numa pesquisa real."

> "A gente usou a pesquisa 04839 do Cesop, que é do Unicamp, coletada em 2023 com 2.000 brasileiros sobre o tema de desigualdade."

---

## Slide 2 — A Pesquisa e as Questões (0:45 – 1:30)

> "A pesquisa trata da percepção dos brasileiros sobre desigualdade. A gente escolheu duas questões específicas:"

> "A primeira é sobre cotas nas universidades: 'A maior presença de pessoas negras e indígenas por meio de cotas é necessária para reduzir a desigualdade?' As opções eram Concorda, Neutro ou Discorda."

> "A segunda é sobre mudanças climáticas: 'Eventos extremos como chuvas e secas afetam mais pessoas em situação de pobreza?' Mesmas opções."

> "A escolha foi intencional: são questões onde o perfil social da pessoa, escolaridade, renda, região, tende a influenciar bastante a resposta."

---

## Slide 3 — Preparação dos Dados (1:30 – 2:15)

> "Do dataset original com 2.000 respondentes, depois de remover valores ausentes e respostas em branco, ficamos com 1.849 registros válidos."

> "As variáveis de perfil que a gente usou foram: sexo, escolaridade agrupada em quatro níveis, renda pessoal em salários mínimos e região do Brasil."

> "As respostas originais tinham cinco opções — de 'Concorda totalmente' a 'Discorda totalmente'. A gente simplificou para três: Concorda, Neutro e Discorda. Isso deixou o problema mais tratável e a comparação mais clara."

---

## Slide 4 — O Modelo e os Prompts (2:15 – 3:30)

> "O modelo escolhido foi o Gemini 1.5 Flash, via Google AI Studio no tier gratuito. A escolha foi por disponibilidade, custo zero e boa capacidade de seguir instruções em português."

> "Pra cada respondente, a gente montou um prompt com o perfil dele e as duas perguntas. Vou mostrar um exemplo:"

> *(mostrar o prompt na tela)*

> "Sexo feminino, 36 anos, ensino médio, renda de 1 a 2 salários mínimos, Centro-Oeste. O modelo recebe isso e responde no formato Q1 e Q2. Se a resposta vier fora das opções válidas, é descartada como nula."

> "Rodamos 3 repetições com amostras diferentes de 200 respondentes cada, pra medir se o modelo é estável ou varia muito entre execuções."

---

## Slide 5 — Resultados (3:30 – 5:00)

> *(preencher com os valores reais após rodar o notebook)*

> "Os resultados mostraram uma acurácia média de [X%] na Q1 e [Y%] na Q2. A variância entre as três rodadas foi de [Z], o que indica que o modelo é [estável / instável]."

> "Olhando a distribuição, o modelo [acertou / superestimou / subestimou] a proporção de respostas 'Concorda' na questão de cotas. Na Q2, sobre mudanças climáticas, a aderência foi [melhor / pior]."

> "Quando a gente quebrou por escolaridade, [grupo X] teve acurácia maior. Isso faz sentido porque [observação baseada nos dados]."

> *(mostrar os gráficos de barras e a matriz de confusão)*

---

## Slide 6 — Conclusão (5:00 – 6:00)

> *(preencher com base nos resultados reais)*

> "De forma geral, o LLM conseguiu capturar [tendência geral], mas teve dificuldade com [grupo ou questão específica]."

> "A principal limitação é que o modelo foi treinado com dados em inglês majoritariamente, então pode ter viés ao simular perfis de brasileiros de baixa renda ou sem escolaridade."

> "Como próximo passo, seria interessante testar com um modelo fine-tuned em dados brasileiros, ou comparar com um Random Forest como o artigo base sugere."

> "O código, os dados e o artigo estão disponíveis no repositório do GitHub. Obrigado."

---

## Dicas de gravação

- Grave a tela do Colab rodando enquanto fala
- Não precisa aparecer, só a tela com o notebook e os gráficos já resolve
- Fala devagar nos slides 4 e 5, são os mais densos
- 6 minutos é folgado, não precisa correr
