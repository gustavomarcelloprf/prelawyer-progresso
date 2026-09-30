# Progresso & Validação

Painel público de acompanhamento dos ajustes, com passo a passo para quem valida.

- `index.html`: página autocontida (sem CDN), no layout v3. Lê o `./progress.json` e guarda as anotações do validador só no navegador dele (localStorage).
- `progress.json`: **o único arquivo que muda a cada tarefa.**

## Como o CLI atualiza

Toda tarefa inclui atualizar o painel: mover o status e escrever os passos. Editar só o `progress.json`, depois `git commit` e `git push`. O Pages republica em cerca de 1 minuto.

```json
{
  "atualizado_em": "30 de setembro de 2026",
  "itens": [
    { "id": "#20", "titulo": "…", "status": "feito",
      "desc": "o que estamos conferindo, numa frase",
      "passos": ["onde ir", "o que clicar", "o que digitar"],
      "esperado": "o que a pessoa deve ver" },
    { "id": "C4", "titulo": "…", "status": "a_fazer" }
  ]
}
```

- `atualizado_em`: texto por extenso, exibido do jeito que está escrito.
- `status`:
  - `a_fazer`: só precisa de `id`, `titulo` e `status`.
  - `em_andamento` ("Em desenvolvimento"): o item entra aqui quando o spec dele é disparado.
  - `feito` ("Pronto para conferir"): precisa de `desc`, `passos` e `esperado`.
  - `validado` ("Conferido"): mantém `desc`, `passos` e `esperado`.
- Os textos entram na página como HTML. Não use `<` nem `>`, e prefira aspas duplas às simples no `id`.
- Português simples, sem jargão técnico e sem dados reais (clientes, CPF/CNPJ, e-mails, endereços do sistema).

## Publicar

Settings → Pages → Deploy from a branch → **gh-pages** / **(root)**. Já está ativo em https://gustavomarcelloprf.github.io/prelawyer-progresso/

Teste local: `python3 -m http.server` nesta pasta e abrir `http://localhost:8000`.
