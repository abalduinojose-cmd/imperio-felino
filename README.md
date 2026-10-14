# Império Felino — vitrine de afiliados Shopee

Site estático (um único `index.html` + pasta `img/`). Não precisa de build nem de servidor especial: qualquer hospedagem de arquivos estáticos serve.

## No ar

- Site: https://www.imperiofelino.com.br/
- Endereço antigo (redireciona para o domínio): https://abalduinojose-cmd.github.io/imperio-felino/
- Repositório: https://github.com/abalduinojose-cmd/imperio-felino

Todo `git push` na branch `main` atualiza o site em cerca de 1 minuto.

## Estrutura

- `index.html` — a página inteira (estilo, produtos e script).
- `img/` — avatar e fotos dos 20 produtos (`p01.jpg` … `p20.jpg`, na mesma ordem do Linktree).

## Editar

**Links do grupo e dos cupons** — no fim de `index.html`, preencha as duas linhas:

```js
var GRUPO_URL = "";   // convite do WhatsApp (https://chat.whatsapp.com/...) ou Telegram
var CUPONS_URL = "";  // página de cupons
```

Enquanto estiverem vazias, os botões mostram a etiqueta "em breve". O botão flutuante "Grupo de ofertas", que aparece ao rolar a página, usa o mesmo `GRUPO_URL`.

**Estatísticas** — no fim de `index.html`, preencha `GA_ID` com o ID de medição do Google Analytics 4 (formato `G-XXXXXXXXXX`). O site registra os eventos `entrar_grupo` (com o local do botão), `clique_produto` (produto, loja e local), `clique_cupom` e `clique_rede_social`. Vazio, nenhum contador é carregado.

**Cupons** — no fim de `index.html`, a lista `CUPONS` tem um cupom por linha: `valor`, `regra`, `onde` e `ate` (fim da validade). Cupom vencido some sozinho do site; se todos vencerem, aparece um aviso de que a Shopee libera cupons novos todo dia. `CUPONS_URL` é o link de todos os cartões de cupom e do botão "Ver todos os cupons" — use o seu link de afiliado da página https://shopee.com.br/m/cupom-de-desconto.

**Produtos** — a lista fica no fim de `index.html`, na constante `PRODUTOS`, uma linha por produto:

```js
{ img:"img/p21.jpg", nome:"Nome do produto", cat:"brinquedos", link:"https://s.shopee.com.br/SEU-LINK" },
```

1. Salve a foto em `img/` (quadrada, ~450px).
2. Acrescente a linha com o seu link de afiliado.
3. `cat` precisa ser uma das chaves de `SECOES`: `natal`, `saude` (Medicamentos), `brinquedos`, `alimentacao`, `casa`, `higiene`, `fofura`. A seção `natal` é sazonal: apague a linha dela em `SECOES` quando a temporada acabar. Para criar uma seção nova, adicione uma chave em `SECOES`; a barra de navegação e a seção aparecem sozinhas. `SECOES_NOTA` mostra um aviso curto embaixo do título de uma seção (hoje usado em Medicamentos).

**Você viu no Instagram** — fica logo depois dos mais procurados. A lista `NO_INSTAGRAM` tem os links dos produtos que apareceram nos vídeos, na ordem de exibição; o produto precisa estar também em `PRODUTOS`. Lista vazia esconde a seção.

**Preços** — cada produto aceita campos opcionais: `preco`, `de` (preço antigo riscado), `desc` (% de desconto), `aPartir: true` (produto com variações), `nota` (ex.: "no Pix com cupom"), `frete: "gratis"` ou `frete: "cupom"`, `freteMin: 80` (frete grátis acima de um valor), `relampago: true`, `estrelas`, `avaliacoes`, `vendidos` e `parcelas: { n: 12, valor: 7.36 }`. Atualize também `PRECOS_EM` com a data da conferência. Os preços da Shopee mudam com frequência; confira antes de divulgar.

**Mais procurados do mês** — são sempre os 6 primeiros da lista. Reordene a lista para mudar o ranking.

## Rodar localmente

```bash
python -m http.server 5500
```

Depois abra http://127.0.0.1:5500 no navegador.

## Publicar e vincular um domínio

Opções gratuitas que aceitam esta pasta do jeito que está:

- **Netlify Drop** (https://app.netlify.com/drop): arrasta a pasta e ganha um endereço `*.netlify.app`. Depois, em *Domain management*, adiciona o seu domínio.
- **Vercel** (https://vercel.com/new): importa a pasta ou o repositório Git; o domínio é configurado em *Settings → Domains*.
- **GitHub Pages**: sobe o repositório no GitHub, ativa Pages na branch `main` e, em *Settings → Pages → Custom domain*, informa o domínio.

Em todos os casos, no painel onde você comprou o domínio (Registro.br, GoDaddy, Hostinger…), crie os registros DNS que a hospedagem indicar (normalmente um `A` ou `CNAME`).
