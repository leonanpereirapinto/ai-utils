# Mem0

- Tecnologia: Python / TypeScript
- Repositório: https://github.com/mem0ai/mem0
- Documentação: https://docs.mem0.ai/

## Para Que Serve

Mem0 é uma camada de memória para assistentes e agentes de IA. Em vez de reenviar todo o histórico a cada interação, ela extrai fatos relevantes de conversas, armazena essas memórias e recupera o que importa no momento da resposta.

Na prática, serve para adicionar memória persistente e personalizada a aplicações com LLMs. O projeto oferece plataforma hosted e opção open source/self-hosted, com SDKs para Python e JavaScript, CLI e API REST. A documentação também cobre recursos como graph memory, filtros por metadados, busca com reranker e suporte multimodal.

## Bons Cenários de Uso

- assistentes que precisam lembrar preferências, perfil e contexto do usuário entre sessões
- agentes de suporte ou sucesso do cliente que devem recuperar histórico relevante sem depender de prompts enormes
- produtos com memória de longo prazo para copilotos, companions ou fluxos de automação
- arquiteturas com múltiplos agentes ou ferramentas compartilhando contexto persistente
- aplicações que precisam combinar memória semântica com filtros por usuário, agente, tags ou categorias

## Observações

- A plataforma hosted é o caminho mais rápido para começar; a versão OSS faz mais sentido quando controle de infraestrutura, privacidade ou customização da stack são prioridades.
- No modo open source, a configuração pode combinar provedores diferentes de LLM, embeddings, reranking e vector store, como Qdrant, Postgres com `pgvector`, OpenAI, Ollama e outros suportados pela documentação.
- Recursos como graph memory e reranker melhoram a recuperação em cenários mais complexos, mas aumentam a complexidade operacional em comparação com uma memória vetorial mínima.
- É uma opção prática quando o problema é memória entre sessões; não substitui, por si só, orquestração de agentes, modelagem de ferramentas ou pipelines completos de RAG.

## Skills Locais

- Nenhuma no momento.
