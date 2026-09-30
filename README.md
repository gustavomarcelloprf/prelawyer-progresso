# Guia de validação (gh-pages)

Branch órfã, sem ligação com `staging` nem `main`. Guarda só o guia de validação dos ajustes.

- `index.html`: página autocontida (sem CDN). Lê o `progress.json` e mostra a visão geral, os itens agrupados por status e, em cada validação, o passo a passo.
- `progress.json`: **o único arquivo que muda a cada sessão.**

## Como o CLI atualiza

Editar só o `progress.json`, depois `git commit` e `git push origin gh-pages`. O Pages republica em cerca de 1 minuto.

- `atualizado_em`: data e hora em ISO 8601.
- `itens[].status`: `pendente` | `em_andamento` | `feito` | `validado` | `erro`
- `itens[].validacoes[]`: `{ acao, passos: [...], esperado, estado, nota }`
  - `estado`: `a_validar` | `ok` | `erro`
  - `nota`: o retorno do validador, escrito por quem coordena.
- `pr` e `flag` ficam no JSON para uso interno. A página **não** os mostra.

Regras do texto: português simples, sem jargão técnico, passos literais (onde ir, o que clicar, o que digitar). Nada de dados reais: nomes de clientes, CPF/CNPJ, e-mails e endereços do sistema ficam de fora.

As marcações que o validador faz na página ficam só no navegador dele (localStorage). Ele usa "Copiar minhas anotações" e envia o texto para quem coordena, que atualiza o `progress.json`.

## Publicar

Settings → Pages → Source: **Deploy from a branch** → Branch **gh-pages** / **(root)** → Save.

Teste local: `python3 -m http.server` nesta pasta e abrir `http://localhost:8000` (o `fetch` não funciona em `file://`).
