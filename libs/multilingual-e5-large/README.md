# Multilingual E5 Large

- Tecnologia: Python (transformers / sentence-transformers)
- Repositório: https://huggingface.co/intfloat/multilingual-e5-large
- Documentação: https://huggingface.co/intfloat/multilingual-e5-large

## Para Que Serve

Multilingual E5 Large é um modelo de embeddings de texto multilíngue da Microsoft com 560M de parâmetros, baseado no XLM-RoBERTa-large. Gera vetores de 1024 dimensões para até 512 tokens e suporta 100 idiomas em tarefas de retrieval, similaridade semântica, classificação e clustering.

O treinamento acontece em dois estágios: pré-treino contrastivo com ~5B de pares de texto fracamente supervisionados (mC4, NLLB, CC News, Wikipedia, Reddit, S2ORC, StackExchange) seguido de fine-tuning supervisionado em datasets como MS MARCO, NQ, Mr. TyDi e MIRACL. A licença é MIT.

## Bons Cenários de Uso

- busca semântica multilíngue em pipelines de RAG com suporte a dezenas de idiomas
- retrieval assimétrico (query curta vs. passagem longa) com prefixos `query:` e `passage:`
- classificação ou clustering de textos multilíngues via embeddings como features
- cenários onde a mesma base vetorial precisa cobrir documentos em múltiplos idiomas

## Observações

- Prefixos são obrigatórios: `query: ` para queries e `passage: ` para documentos em retrieval; para tarefas simétricas (similaridade, clustering), usar `query: ` em ambos os lados. Sem prefixo a performance degrada significativamente.
- A similaridade cosseno costuma ficar entre 0.7 e 1.0 (não 0 a 1) por causa da temperatura baixa (0.01) na loss InfoNCE — o que importa é a ordenação relativa, não valores absolutos.
- Textos acima de 512 tokens são truncados; para documentos longos é necessário chunking antes de gerar embeddings.
- Idiomas de alto recurso (inglês, chinês, espanhol) performam melhor; idiomas de baixo recurso podem ter degradação.
- Existe a variante `multilingual-e5-large-instruct` que aceita instruções customizadas em vez de prefixos fixos.
- Disponível em PyTorch, Safetensors, ONNX e OpenVINO; a comunidade mantém 26 quantizações e 159 fine-tunes.

## Skills Locais

- Nenhuma no momento.
