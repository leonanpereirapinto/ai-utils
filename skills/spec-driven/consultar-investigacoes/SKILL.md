---
name: consultar-investigacoes
description: Responde perguntas sobre um repositório com base nos artefatos gerados por `mapear-projeto`, `investigar-area` e `consolidar-investigacoes`. Use quando o usuário quiser consultar, resumir, explicar, comparar achados, recuperar evidências, identificar riscos, listar lacunas ou orientar próximos passos a partir de `project-map.md`, `investigation-backlog.md`, arquivos de task, arquivos de resultado ou `project-map-consolidated.md`. Não use para gerar novos artefatos, executar investigações, nem validar o código-fonte diretamente.
---

# Consulta Baseada em Investigacoes

## Procedimento

**Passo 1: Localizar o corpus de artefatos**
1. Confirmar se o usuário forneceu um caminho explícito para `project-map-consolidated.md`, `project-map.md` ou para o diretório `./tasks/project-map-[project-slug]/`.
2. Se nenhum caminho for fornecido, inferir o diretório de trabalho mais provável em `./tasks/project-map-[project-slug]/`.
3. Procurar os artefatos descritos em [references/artefatos-gerados.md](references/artefatos-gerados.md).
4. Se nenhum artefato existir, interromper e orientar o usuário a executar `mapear-projeto` primeiro.

**Passo 2: Montar o contexto mínimo para a pergunta**
1. Classificar a pergunta do usuário: visão geral, detalhe de uma task, riscos transversais, lacunas, evidências, contradições ou próximos passos.
2. Ler primeiro o menor conjunto de artefatos suficiente para responder.
3. Se `project-map-consolidated.md` existir, usá-lo como ponto de entrada para perguntas amplas.
4. Se a pergunta citar uma task ou área específica, ler a task correspondente e o respectivo arquivo em `results/`.
5. Se a pergunta pedir cobertura, pendências ou ordem de execução, ler `investigation-backlog.md` junto com `tasks/` e `results/`.

**Passo 3: Responder com rastreabilidade**
1. Basear a resposta apenas nos artefatos gerados, não em inspeção livre do código.
2. Separar claramente:
   - fatos confirmados pelos artefatos
   - inferências razoáveis feitas ao combinar artefatos
   - lacunas ou pontos não respondidos.
3. Citar caminhos de arquivo e IDs de task para toda afirmação importante.
4. Se a resposta depender de uma conclusão consolidada, indicar isso explicitamente.
5. Se uma conclusão detalhada vier de um resultado individual, preservar a referência ao arquivo `results/[id]-[area-slug]-result.md`.

**Passo 4: Resolver conflitos e profundidade**
1. Em caso de conflito entre artefatos, manter a divergência explícita.
2. Preferir a evidência mais profunda e mais específica:
   - `results/[id]-[area-slug]-result.md`
   - `tasks/[nn]-[area-slug].md`
   - `investigation-backlog.md`
   - `project-map.md`
3. Tratar `project-map-consolidated.md` como síntese de entrada para perguntas amplas, mas voltar aos artefatos-fonte quando for preciso confirmar detalhes, exceções ou contradições.
4. Não esconder inconsistências entre o consolidado e os resultados individuais.

**Passo 5: Fechar com próximo passo útil**
1. Se os artefatos responderem bem à pergunta, encerrar com uma síntese curta e evidências-chave.
2. Se os artefatos forem insuficientes, dizer exatamente o que falta.
3. Recomendar a próxima skill correta:
   - `mapear-projeto` para ausência do mapa inicial
   - `investigar-area` para uma área ainda não aprofundada
   - `consolidar-investigacoes` para perguntas transversais quando ainda não existir consolidação.

## Heuristicas de Consulta

- Para "como o projeto se organiza?", priorizar `project-map-consolidated.md`; na falta dele, usar `project-map.md`.
- Para "o que a task 03 descobriu?", ler `tasks/03-*.md` e `results/03-*-result.md`.
- Para "quais riscos transversais existem?", combinar `project-map-consolidated.md` com os resultados individuais quando necessário.
- Para "quais investigações faltam?", comparar `investigation-backlog.md` com os arquivos presentes em `results/`.
- Para "qual é a evidência de X?", localizar a afirmação no artefato mais específico e citar o caminho correspondente.

## Diretrizes

- Responder primeiro à pergunta; detalhar a trilha de evidências em seguida.
- Manter o foco no corpus gerado pelas skills, não no restante do repositório.
- Preservar IDs de task, nomes de áreas e caminhos para facilitar auditoria.
- Assumir o mínimo possível quando os artefatos estiverem incompletos.
- Explicitar quando uma conclusão for inferida a partir da combinação de múltiplos documentos.

## Checklist de Qualidade

- [ ] Artefatos corretos localizados ou inferidos.
- [ ] Menor conjunto de documentos lido para responder com segurança.
- [ ] Resposta ancorada em evidências dos artefatos.
- [ ] Conflitos e lacunas explicitados.
- [ ] Próximo passo recomendado quando o corpus for insuficiente.

## Tratamento de Erros

- Se `project-map.md` não existir, orientar o usuário a executar `mapear-projeto`.
- Se uma task específica não tiver resultado, informar a ausência e sugerir `investigar-area`.
- Se a consolidação estiver ausente para uma pergunta transversal, responder com o corpus disponível e sugerir `consolidar-investigacoes` quando isso reduzir ambiguidade.
- Se o usuário pedir validação contra o código-fonte, informar que isso está fora do escopo desta skill e só prosseguir se ele mudar explicitamente a solicitação.
