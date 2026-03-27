# Ferramentas, Conceitos e Técnicas de Busca Vetorial

- Fonte: Blink "A Ciência por Trás da Busca Vetorial", baseado no curso de Daniel Romero
- Data de revisão: 2026-03-27
- Tópico: pipeline de retrieval para busca vetorial

## Resumo

Esta nota resume um pipeline prático de retrieval para busca vetorial. A ideia central é que um sistema bom não depende de um único modelo de embedding, mas da combinação entre chunking, recuperação densa e esparsa, fusão de rankings, re-ranking e filtros por metadados. O material apresenta busca vetorial como um problema de desenho incremental, em que cada camada corrige uma limitação clara da camada anterior.

## Pontos-chave

- Ferramentas citadas: `Qdrant` como banco vetorial, `FastEmbed` para geração de embeddings, `edgartools` com a API `EDGAR`/`SEC` para ingestão de documentos e `Python` como camada de orquestração.
- A busca densa usa modelos como `all-MiniLM-L6-v2` e compara vetores de query e documento com similaridade cosseno para capturar proximidade semântica.
- A busca esparsa usa `BM25` como evolução do `TF-IDF` para valorizar correspondência exata de termos, o que é especialmente útil para nomes, tickers, datas e termos técnicos.
- Similaridade e relevância não são a mesma coisa: um documento pode ser semanticamente próximo da query e ainda assim não responder à intenção real do usuário.
- `Hybrid search` executa busca densa e esparsa em paralelo e depois combina os candidatos para melhorar recall e relevância prática.
- `Reciprocal Rank Fusion (RRF)` combina rankings pela posição dos documentos, e não pelos scores brutos, o que evita o problema de escalas diferentes entre `BM25` e busca vetorial.
- O re-ranking com `ColBERT` usa interação tardia entre tokens da query e do documento; o material também o contrasta com `cross-encoders`, que tendem a ser mais lentos.
- O `Qdrant` aparece como peça importante porque suporta vetores densos, esparsos e multi-vetores no mesmo documento, além de orquestrar `prefetch`, fusão e re-ranking no lado do servidor.
- `Semantic chunking` agrupa parágrafos por significado, e não por posição no texto, usando embeddings, `HDBSCAN` e limite de tokens por chunk.
- `HDBSCAN` é usado porque consegue inferir a estrutura dos clusters automaticamente, trabalha com noção de densidade no espaço vetorial e se beneficia de distância Euclidiana com tratamento explícito de órfãos.
- Metadados estruturados como empresa, data e tipo de relatório transformam o banco vetorial em uma base filtrável, e não apenas em um índice de similaridade.

## Por que importa

- Oferece um blueprint concreto para construir sistemas de RAG e busca com mais qualidade do que uma solução baseada apenas em embeddings densos.
- Mostra onde correspondência exata, filtros por metadados e re-ranking por token melhoram de forma real a qualidade do retrieval em domínios especializados.
- Reforça um padrão de implementação prático: recuperar rápido primeiro e gastar mais custo computacional apenas no conjunto pequeno de candidatos sobreviventes.

## Cuidados

- A progressão de scores citada no material (`60%` com busca densa, `66%` com hybrid search + `RRF` e relevância máxima normalizada após `ColBERT`) depende do dataset e da forma de avaliação usada no curso.
- `Semantic chunking`, `HDBSCAN` e `ColBERT` aumentam complexidade, esforço de ajuste e latência, então devem ser introduzidos de forma incremental e medidos no domínio real.
- O texto é um resumo de curso, não um guia completo de implementação, então vários detalhes operacionais aparecem de forma condensada.

## Lembrete rápido

Pipeline recomendado: semantic chunking -> armazenamento de vetores densos, esparsos e metadados no `Qdrant` -> retrieval híbrido -> fusão com `RRF` -> re-ranking com `ColBERT` sobre os melhores candidatos.
