# AGENTS.md

## Objetivo

Este repositório funciona como um acervo curado de materiais úteis para trabalho com IA. Ele não deve ser tratado como um único app ou pacote, e sim como uma base organizada de:

- referências de bibliotecas em `libs/`
- notas de estudo em `study-notes/`
- skills customizadas em `spec-driven-custom/`

## Regras Gerais

- Mantenha a raiz do projeto enxuta. Novos conteúdos devem entrar nas áreas já existentes sempre que possível.
- Antes de criar arquivos novos, leia os arquivos vizinhos e siga o padrão local de estrutura, idioma e nível de detalhe.
- Prefira conteúdo curto, escaneável e orientado a uso prático.
- Não duplique material. Se algo já existir, complemente, reorganize ou referencie.
- Preserve o idioma predominante do arquivo ou diretório em que estiver trabalhando.
- Não adicione arquivos temporários, dumps, saídas geradas ou artefatos sem valor duradouro.

## Como Organizar `libs/`

- Cada biblioteca deve viver em sua própria pasta, em `libs/<nome-da-lib>/`.
- Cada pasta de biblioteca deve ter um `README.md` próprio.
- Use `libs/README.template.md` como base para novas entradas.
- O README local deve explicar:
  - o que a biblioteca faz
  - em quais cenários ela é útil
  - observações importantes, limites ou diferenciais
  - links para repositório e documentação oficial
- Se houver skills locais relacionadas, elas devem ficar em `libs/<nome-da-lib>/skills/`.
- Sempre atualize o índice em `libs/README.md` quando adicionar, remover ou renomear bibliotecas.
- Prefira nomes de pasta estáveis e simples, normalmente em minúsculas.

## Como Organizar `study-notes/`

- Use `study-notes/docs/` para notas derivadas de documentação, papers, guias ou fontes externas.
- Use `study-notes/explanations/` para conceitos, comparações, trade-offs e orientações práticas.
- Use os templates em `study-notes/templates/` ao criar novas notas.
- Notas de documentação devem registrar fonte, link, data de revisão e tópico.
- Cada arquivo deve cobrir um assunto bem delimitado.
- Se uma nota crescer demais, divida em arquivos menores.

## Como Organizar `spec-driven-custom/`

- Esta área guarda skills reutilizáveis para fluxos guiados por especificação.
- Use `skills-core/` para skills principais do fluxo de trabalho.
- Use `skills-tests/` para skills de teste, QA, acessibilidade ou navegação assistida.
- Cada skill deve ter uma pasta própria com `SKILL.md` obrigatório.
- Pastas auxiliares como `assets/`, `references/` e `scripts/` só devem existir quando forem realmente usadas pela skill.
- Se um `SKILL.md` mencionar arquivos auxiliares, os caminhos e nomes devem permanecer consistentes.
- Prefira templates e referências reutilizáveis a instruções duplicadas em várias skills.

## Checklist de Mudança

Ao adicionar uma nova biblioteca:

- crie `libs/<nome>/README.md`
- siga `libs/README.template.md`
- atualize `libs/README.md`
- inclua `skills/` apenas se houver material local relevante

Ao adicionar uma nova nota:

- escolha entre `docs/` e `explanations/`
- use o template apropriado
- mantenha o conteúdo curto e útil

Ao adicionar uma nova skill:

- crie uma pasta dedicada
- adicione `SKILL.md`
- inclua apenas os diretórios auxiliares necessários
- verifique se exemplos, assets e referências estão coerentes com o texto da skill

## Padrão de Qualidade

- Prefira links para fontes primárias ou documentação oficial.
- Escreva para consulta rápida, não para marketing.
- Explique sempre o valor prático do conteúdo.
- Use Markdown simples, com títulos claros e listas objetivas.
- Quando houver impacto estrutural, atualize links internos e READMEs relacionados.
