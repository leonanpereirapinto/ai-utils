# FastEmbed

- Tecnologia: Python
- Repositório: https://github.com/qdrant/fastembed
- Documentação: https://qdrant.tech/documentation/fastembed/

## Para Que Serve

FastEmbed é uma biblioteca Python mantida pela Qdrant para gerar embeddings localmente de forma rápida e leve, com foco em inferência via ONNX e integração simples em pipelines de busca vetorial.

No contexto de Qdrant, ela é especialmente útil porque o `qdrant-client` consegue usar FastEmbed diretamente nos fluxos de ingestão e consulta. Isso reduz o código de cola para calcular vetores compatíveis com o modelo escolhido e facilita trabalhar com embeddings densos, esparsos, late interaction, imagem e reranking no mesmo ecossistema.

## Bons Cenários de Uso

- prototipar busca semântica local com `QdrantClient(":memory:")`
- indexar documentos no Qdrant sem montar um pipeline separado de embeddings
- combinar dense retrieval, sparse retrieval e reranking em uma mesma stack
- usar embeddings locais quando privacidade, custo ou latência importam
- explorar busca multimodal ou late interaction com modelos compatíveis

## Observações

- Para integração direta com o cliente do Qdrant, o caminho mais prático é instalar `qdrant-client[fastembed]`; em `zsh`, use aspas no extra.
- O `qdrant-client` pode inferir embeddings implicitamente com `models.Document` e usar `client.get_embedding_size(model_name)` para criar coleções com dimensão correta.
- O foco principal é inferência leve em CPU, mas o projeto também cobre cenários com GPU e modelos adicionais.
- FastEmbed faz mais sentido quando você quer manter a geração de embeddings próxima do cliente ou do pipeline de ingestão, em vez de depender de um serviço separado.

## Skills Locais

- Nenhuma no momento.
