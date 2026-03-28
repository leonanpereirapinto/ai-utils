# Building Effective Agents

- Fonte: artigo técnico da Anthropic
- Link: https://www.anthropic.com/engineering/building-effective-agents
- Publicado em: 2024-12-19
- Data de revisão: 2026-03-28
- Tópico: padrões de sistemas agênticos com LLMs

## Resumo

O artigo da Anthropic defende uma regra simples: comece pela solução mais simples possível e só adicione comportamento agêntico quando isso melhorar o resultado de forma mensurável. A distinção central é entre `workflows`, onde o caminho é definido por código, e `agents`, onde o modelo decide dinamicamente como usar ferramentas e como avançar. A proposta prática é subir em complexidade aos poucos, saindo de um `augmented LLM` para workflows compostos e, só quando necessário, para agentes autônomos.

## Pontos-chave

- O bloco base é o `augmented LLM`: um modelo com acesso a `retrieval`, ferramentas e memória. O ganho real depende menos do framework e mais de uma interface de ferramentas clara, bem documentada e fácil de usar pelo modelo.
- `Prompt chaining` serve para tarefas com etapas fixas e decomposição limpa; `routing` serve para classificar entradas e encaminhá-las para prompts, ferramentas ou modelos especializados.
- `Parallelization` ajuda quando subtarefas são independentes ou quando vale comparar múltiplas tentativas; a Anthropic divide isso em `sectioning` e `voting`.
- `Orchestrator-workers` faz sentido quando não dá para prever de antemão quais subtarefas serão necessárias, como em mudanças de código espalhadas por vários arquivos ou buscas abertas em múltiplas fontes.
- `Evaluator-optimizer` é útil quando há critério claro de qualidade e a resposta melhora com iteração guiada por feedback estruturado.
- `Agents` entram quando o número de passos é imprevisível, o sistema precisa decidir a próxima ação com base no ambiente e existem maneiras de obter `ground truth` ao longo da execução, como resultados de ferramentas, testes ou execução de código.
- A Anthropic recomenda evitar abstrações demais no início: frameworks aceleram prototipagem, mas também podem esconder prompts, respostas e erros, o que dificulta depuração e incentiva complexidade prematura.
- No apêndice sobre ferramentas, a mensagem principal é que `tool design` também é prompt engineering: escolha formatos naturais para o modelo, reduza overhead de formatação, inclua exemplos, deixe limites explícitos e teste a ferramenta até torná-la difícil de usar errado.

## Por que importa

- Dá um critério melhor para decidir entre prompt simples, workflow e agente, em vez de tratar tudo como "agente" por padrão.
- Ajuda a desenhar sistemas mais confiáveis, porque liga autonomia a observabilidade, feedback do ambiente, guardrails e critérios de parada.
- Reforça uma ideia prática importante: em produção, clareza de ferramentas, avaliação e transparência costumam pesar mais do que sofisticar a arquitetura cedo demais.

## Cuidados

- O texto é um guia prático baseado na experiência da Anthropic, não uma taxonomia definitiva nem uma prova de que uma arquitetura sempre supera a outra.
- Agentes autônomos aumentam custo, latência e risco de erro acumulado; em muitos casos, uma chamada única com bom contexto, `retrieval` e exemplos já resolve o problema.
- Sem feedback verificável do ambiente, checkpoints humanos e limites explícitos de execução, a autonomia do agente tende a ficar mais frágil e difícil de controlar.

## Lembrete rápido

Regra prática: comece com `single LLM call + retrieval + exemplos`; use `workflow` quando o caminho puder ser definido; use `agent` quando os passos forem imprevisíveis, houver feedback real do ambiente e você conseguir testar, limitar e inspecionar o processo.
