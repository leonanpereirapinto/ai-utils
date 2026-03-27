# Docling

- Tecnologia: Python
- Repositório: https://github.com/docling-project/docling
- Documentação: https://docling-project.github.io/docling/

## Para Que Serve

Docling é um toolkit de processamento de documentos focado em transformar diferentes formatos de entrada em saídas estruturadas, mais fáceis de usar em pipelines de IA.

Ele é especialmente forte em parsing de PDFs, mas também suporta formatos como DOCX, PPTX, XLSX, HTML, Markdown, texto puro, imagens, áudio e arquivos de legenda. Pode rodar localmente, exportar para formatos como Markdown, HTML e JSON, e é útil quando OCR, ordem de leitura, tabelas ou estrutura do documento importam.

## Bons Cenários de Uso

- ingestão de documentos em pipelines de RAG ou busca
- conversão de PDFs e arquivos de escritório para Markdown ou JSON
- extração de conteúdo sensível a layout, como tabelas, títulos e seções
- OCR de documentos digitalizados
- processamento em lote de coleções de documentos
- preparação de conteúdo normalizado para fluxos posteriores com LLMs

## Observações

- É uma opção forte quando processamento local importa por privacidade ou restrições de ambiente.
- Inclui APIs em Python, CLI e suporte a MCP para fluxos com agentes.
- O suporte a chunking ajuda quando o documento precisa ser dividido para recuperação ou embeddings.

## Skills Locais

- [Beagle Docling Skill](./skills/beagle-docling/SKILL.md)
