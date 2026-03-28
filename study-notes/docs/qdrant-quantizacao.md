# Quantização no Qdrant

- Fonte: artigo "What is Vector Quantization?" e documentação oficial de quantização do Qdrant
- Link 1: https://qdrant.tech/articles/what-is-vector-quantization/
- Link 2: https://qdrant.tech/documentation/manage-data/quantization/
- Data de revisão: 2026-03-28
- Tópico: quantização vetorial no Qdrant

## Resumo

Quantização no Qdrant comprime embeddings para reduzir uso de RAM e acelerar busca aproximada, sem descartar os vetores originais. Na prática, o banco usa os vetores quantizados para recuperar candidatos rapidamente e pode recuperar precisão com `rescore` e `oversampling`. `Scalar` é a escolha mais segura como padrão; `binary` é a mais agressiva em ganho de memória e velocidade; `product` faz sentido quando memória é a restrição principal e perda de qualidade é aceitável.

## Pontos-chave

- O problema atacado é custo de memória e I/O: um embedding de `1536` dimensões em `float32` ocupa cerca de `6 KB`, então `1` milhão de vetores já consome algo em torno de `6 GB`.
- No Qdrant, vetores quantizados ficam armazenados junto dos vetores originais, o que permite trocar estratégia de quantização, comparar resultados e fazer `rescore` sem reingerir os dados.
- `Scalar quantization` converte componentes `float32` para `int8`, reduz o footprint em `4x` e costuma preservar bem a qualidade. É a opção padrão mais universal.
- O parâmetro `quantile` em `scalar` ajusta os limites da quantização para lidar com outliers. Ele afeta precisão, não footprint.
- `Binary quantization` transforma cada dimensão em bits e pode chegar a `32x` de compressão e até `40x` de ganho de velocidade em modelos compatíveis.
- `Binary` não é universal: funciona melhor com vetores de alta dimensionalidade e distribuição centrada. A documentação cita bons resultados com modelos testados como `text-embedding-ada-002` e `embed-english-v2.0`.
- Para vetores menores ou medianos, a documentação recomenda considerar `1.5-bit`, `2-bit` e quantização assimétrica, disponíveis a partir do Qdrant `v1.15.0`, para recuperar precisão sem voltar ao custo total do `float32`.
- `Product quantization` divide o vetor em segmentos e representa cada parte por índices de centróides. Pode comprimir mais do que `scalar`, chegando a `64x`, mas é mais lenta e perde mais qualidade.
- Em query time, os controles principais são `rescore`, `oversampling` e `ignore`. `rescore` usa os vetores originais para reavaliar o top-k, `oversampling` amplia o conjunto inicial de candidatos e `ignore: true` permite comparar a busca sem quantização.
- Para reduzir RAM de verdade, não basta ativar quantização. O cenário híbrido recomendado é manter vetores originais em disco com `vectors.on_disk: true` e vetores quantizados em RAM com `always_ram: true`.

## Por que importa

- Ajuda a viabilizar coleções grandes em infra mais barata, sem perder a opção de refinar o ranking com os vetores originais.
- Afeta decisões de modelo, dimensionalidade, layout de armazenamento e parâmetros de busca no Qdrant.
- Dá um caminho prático para medir trade-off real entre custo, latência e recall em vez de tratar quantização como um ajuste cego.

## Cuidados

- Ativar quantização sem mover os vetores originais para disco pode preservar quase todo o custo de RAM, então confira a configuração de armazenamento.
- `Binary` entrega os maiores ganhos, mas pode degradar a qualidade em modelos não compatíveis ou vetores pouco dimensionais; nesse caso, `scalar` costuma ser o baseline mais seguro.
- `Product` é atraente no papel por comprimir muito, mas a própria documentação ressalta perda significativa de acurácia e menor velocidade do que `scalar`.
- O ajuste de `oversampling` e `rescore` depende do caso real. O melhor caminho é comparar resultados quantizados e não quantizados usando `ignore: true` durante benchmark.

## Lembrete rápido

Regra prática: comece com `scalar + quantile` ajustado, teste `binary + rescore + oversampling` só em modelos compatíveis e use `product` apenas quando memória pesar mais do que latência e precisão.
