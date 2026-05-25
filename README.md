# Simulação de Opinião Pública com LLMs

Projeto da disciplina de Inteligência Artificial, Mackenzie 2026/1  
Professor: Rogerio Oliveira | Turma: CC 7G

## Alunos

- Matheus Henrique de Oliveira Santos - RA 10409051
- Marina Cantarelli Barroca - RA 10740412

## Descrição

Simulação de respostas de pesquisa de opinião pública usando LLM, comparando as distribuições simuladas com os dados reais da pesquisa Cesop 04839.

A pesquisa usada foi a **04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade** (Cesop/Unicamp, 2023), com foco nas questões:
- Q1 (P6B): Cotas nas universidades para negros e indígenas (Concorda / Neutro / Discorda)
- Q2 (P6E): Mudanças climáticas afetam mais pessoas em situação de pobreza (Concorda / Neutro / Discorda)

## Modelo LLM

O projeto usa **Groq** com o modelo **Llama 3.1 70B Versatile** (`llama-3.3-70b-versatile`).

Originalmente o projeto foi iniciado com Google Gemini (`gemini-2.5-flash-lite`), mas a quota gratuita observada foi de apenas 20 requisições/dia (abaixo do limite documentado de 1.000/dia), inviabilizando a execução completa. A migração para Groq, que oferece 30 req/min sem limite diário restritivo, permitiu concluir o experimento.


## Referência principal

Argyle, L. P. et al. *Simulating Public Opinion: Comparing Distributional and Individual-Level Predictions from LLMs and Random Forests*.

CESOP/UNICAMP. *04839 - Percepção dos Brasileiros sobre Temas Relacionados à Desigualdade*, 2023. Disponível em: https://www.cesop.unicamp.br
