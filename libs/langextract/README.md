# LangExtract

- Tecnologia: Python
- Repositório: https://github.com/google/langextract
- Documentação e exemplos: https://github.com/google/langextract/tree/main/docs/examples

## Para Que Serve

LangExtract é uma biblioteca Python para extrair informações estruturadas de texto não estruturado com modelos de linguagem, mantendo cada extração ancorada no trecho original da fonte.

Ela é útil quando você precisa de saídas em formato próximo de schema a partir de relatórios, notas, documentos ou coleções longas de texto, mas ainda quer rastreabilidade até o trecho exato que originou cada extração.

## Bons Cenários de Uso

- extração de medicamentos, diagnósticos, sintomas ou outros campos em notas clínicas
- estruturação de relatórios jurídicos, operacionais ou de negócio
- extração de entidades e relações em documentos longos
- fluxos de revisão em que cada extração precisa permanecer ligada ao texto-fonte
- geração de saídas JSONL anotadas e visualizações HTML para validação
- tarefas de extração few-shot sem necessidade de fine-tuning

## Observações

- É mais adequado para extração ancorada na fonte do que para simples sumarização.
- Suporta modelos em nuvem, como Gemini e OpenAI, além de modelos locais via Ollama.
- Pode processar documentos longos com chunking, paralelismo e extração em múltiplas passagens.
- O suporte a visualização é útil quando os dados extraídos precisam ser revisados por humanos.

## Skills Locais

- [Aeonbridge LangExtract Skill](./skills/aeonbridge-langextract/SKILL.md)
