# Pydantic

- Tecnologia: Python
- Repositório: https://github.com/pydantic/pydantic
- Documentação: https://docs.pydantic.dev/latest/

## Para Que Serve

Pydantic é uma biblioteca Python para validar, converter, serializar e documentar dados a partir de type hints. Ela permite declarar modelos com `BaseModel`, validar payloads vindos de APIs, arquivos, filas ou outras integrações e receber erros estruturados quando o dado de entrada não atende ao schema esperado.

Além de modelos completos, a biblioteca também cobre validação de tipos isolados com `TypeAdapter`, geração de JSON Schema, serialização para Python/JSON e integração com dataclasses. Na prática, ela é uma peça comum em APIs, configuração de aplicações e pipelines em que contratos de dados precisam ser explícitos.

## Bons Cenários de Uso

- validar entrada e saída de APIs ou handlers internos com contratos tipados
- normalizar dados vindos de JSON, variáveis de ambiente, filas ou arquivos
- gerar JSON Schema para documentação, ferramentas ou integração com OpenAPI
- aplicar validação estruturada em pipelines com LLMs ou extração de dados
- serializar modelos de domínio para transporte, armazenamento ou logging
- validar listas, unions e tipos avulsos sem criar um `BaseModel`, usando `TypeAdapter`

## Observações

- No ecossistema atual do Pydantic v2, gestão de configurações baseada em `BaseSettings` foi movida para o pacote separado `pydantic-settings`.
- O comportamento padrão pode fazer coerções úteis de tipo; quando o contrato precisa rejeitar conversões implícitas, vale usar `strict mode`.
- Para JSON bruto, a documentação destaca `model_validate_json()` como caminho mais direto do que fazer `json.loads(...)` antes da validação.
- A biblioteca se apoia em `pydantic-core`, então costuma entregar boa performance sem abrir mão de mensagens de erro detalhadas.

## Skills Locais

- Nenhuma no momento.
