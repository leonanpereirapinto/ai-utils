# Artefatos Gerados pelas Skills de Investigação

## Layout Esperado

Os artefatos normalmente vivem em `./tasks/project-map-[project-slug]/`:

- `project-map.md`
- `investigation-backlog.md`
- `tasks/[nn]-[area-slug].md`
- `results/[nn]-[area-slug]-result.md`
- `project-map-consolidated.md`

## Papel de Cada Artefato

| Artefato | Papel principal | Quando priorizar |
|----------|-----------------|------------------|
| `project-map.md` | Mapa geral breadth-first do repositório | Perguntas amplas quando não houver consolidação |
| `investigation-backlog.md` | Inventário das áreas, prioridades e dependências | Cobertura, pendências e ordem de execução |
| `tasks/[nn]-[area-slug].md` | Escopo, perguntas e sucesso esperado de cada investigação | Entender o limite e a intenção de uma task |
| `results/[nn]-[area-slug]-result.md` | Evidência mais profunda sobre uma área específica | Perguntas detalhadas, contradições e confirmação de achados |
| `project-map-consolidated.md` | Síntese transversal do mapa e dos resultados | Perguntas de onboarding, visão integrada e riscos cruzados |

## Ordem de Prioridade

Usar esta ordem ao resolver conflitos entre artefatos-fonte:

1. `results/[nn]-[area-slug]-result.md`
2. `tasks/[nn]-[area-slug].md`
3. `investigation-backlog.md`
4. `project-map.md`

Usar `project-map-consolidated.md` como ponto de entrada para perguntas amplas e como síntese navegável, mas voltar aos artefatos-fonte quando for preciso confirmar detalhes.

## Roteamento Rápido por Tipo de Pergunta

- Estrutura geral do projeto: `project-map-consolidated.md` ou `project-map.md`
- Status de cobertura: `investigation-backlog.md` + diretório `results/`
- Descobertas de uma task: `tasks/[nn]-[area-slug].md` + `results/[nn]-[area-slug]-result.md`
- Riscos transversais: `project-map-consolidated.md` + resultados individuais relevantes
- Evidência de uma afirmação: artefato mais específico que contenha a conclusão
