# Trafilatura

- Tecnologia: Python
- Repositório: https://github.com/adbar/trafilatura
- Documentação: https://trafilatura.readthedocs.io/

## Para Que Serve

Trafilatura é uma biblioteca Python com CLI para descoberta, coleta e extração de conteúdo textual na Web. Ela transforma HTML bruto em saídas mais úteis para consumo posterior, com foco em texto principal, metadados e, opcionalmente, comentários.

Além da extração em si, o projeto cobre partes práticas do fluxo de aquisição de conteúdo: busca de links via sitemaps e feeds, crawling focado, downloads, limpeza de páginas e exportação em formatos como TXT, Markdown, JSON, CSV, HTML, XML e XML-TEI. Isso faz dela uma opção forte quando o objetivo é reduzir ruído de páginas web antes de indexar, analisar ou reutilizar o conteúdo.

## Bons Cenários de Uso

- extrair artigos, posts e páginas editoriais preservando título, autor, data e corpo principal
- preparar conteúdo web para RAG, busca, sumarização ou pipelines de NLP
- converter HTML já baixado em Markdown, JSON ou XML para processamento posterior
- rastrear sites a partir de sitemap, feed RSS/Atom/JSON ou crawling focado
- processar lotes de URLs ou arquivos HTML com CLI em fluxos de coleta e normalização

## Observações

- O projeto combina API Python e ferramenta de linha de comando, o que ajuda tanto em scripts quanto em processamento operacional em lote.
- A extração é configurável, com opções para favorecer precisão ou recall, filtrar por idioma e incluir elementos como tabelas, links, imagens e comentários.
- Há módulos opcionais para melhorar velocidade e capacidades auxiliares, como detecção de idioma, extração de datas, compressão adicional e downloads mais rápidos.
- A série `2.x` mudou parte da API: `bare_extraction()` passou a retornar um objeto `Document` por padrão, então vale revisar integrações antigas ao atualizar.

## Skills Locais

- Nenhuma no momento.
