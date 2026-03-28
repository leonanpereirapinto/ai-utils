# HTTPie

- Tecnologia: Python
- Repositório: https://github.com/httpie/cli
- Documentação: https://httpie.io/docs/cli/

## Para Que Serve

HTTPie é um cliente HTTP de linha de comando voltado a teste, depuração e uso interativo de APIs, servidores HTTP e web services. O foco do projeto é tornar requisições mais legíveis e ergonômicas no terminal, com sintaxe natural, saída formatada e suporte nativo a JSON.

Ele cobre desde chamadas rápidas até fluxos mais recorrentes, com suporte a headers customizados, autenticação, sessões persistentes, uploads, downloads no estilo `wget`, proxies, HTTPS, streaming e plugins. O ecossistema HTTPie também inclui clientes Web/Desktop, mas o núcleo open source mais consolidado continua sendo a CLI.

## Bons Cenários de Uso

- testar endpoints REST rapidamente no terminal sem montar scripts maiores
- inspecionar respostas JSON com saída colorida e formatada
- repetir chamadas autenticadas usando sessões persistentes
- enviar formulários, arquivos e headers customizados durante debugging de integrações
- baixar artefatos ou respostas grandes com modo de download
- automatizar chamadas HTTP simples em scripts e tarefas operacionais

## Observações

- É mais forte como ferramenta interativa de terminal do que como SDK embutido em aplicações.
- A documentação oficial lista suporte a Linux, macOS, Windows e FreeBSD, além de múltiplos métodos de instalação.
- O sistema de plugins permite estender autenticação, transporte e formatação, mas boa parte desses plugins é mantida pela comunidade.
- O site principal também destaca clientes Web/Desktop; se o objetivo for colaboração visual ou exploração manual de APIs, vale olhar essa parte do ecossistema.

## Skills Locais

- Nenhuma no momento.
