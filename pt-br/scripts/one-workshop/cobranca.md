---
description: Como a oficina cobra acessórios, cores e skins (dinheiro, itens, gemas ou à escolha do jogador) e como ligar as gemas do seu servidor.
---

# Cobrança: dinheiro, itens e gemas

## Forma de cobrar por categoria

Em `Config.Pricing`, cada categoria tem uma forma:

| Forma | O que acontece |
|---|---|
| `'item'` | Só com itens. Acessórios pedem o item de `Config.Items`; a cor pede `Config.PaintItem`; skins pedem os `items` do preço. |
| `'money'` | Só dinheiro, das contas de `accounts` (na ordem). |
| `'gems'` | Só gemas. |
| `'hybrid'` | O jogador escolhe entre as formas que o preço tem. |
| `'free'` | Não cobra. |

```lua
Config.Pricing = {
	accounts = { 'cash', 'bank' },
	parts = 'item',      -- acessórios e acabamentos do jogo
	paint = 'item',      -- cor da arma
	skins = 'hybrid'     -- pacote de skins
}
```

No modo `hybrid`, a barra de baixo da bancada mostra o total em cada forma e o jogador clica na que quer usar. A
cobrança é feita no servidor e é tudo-ou-nada: se algo falhar no meio, o que já saiu volta.

## Preços

```lua
Config.Prices = {
	parts = {
		default = { cash = 4000, gems = 20 },
		['muzzle.supp'] = { cash = 6500, gems = 32 },   -- tipo exato
		scope = { cash = 5000, gems = 25 },             -- família
	},
	paint = { cash = 1500, gems = 8 }
}
```

Nos acessórios, o preço em itens vem de `Config.Items` (um item por peça). `false` deixa a peça ou a cor livre.

### Preço por bancada

Uma bancada pode ter desconto ou acréscimo: `prices = { skins = 0.8, parts = 1.2 }` em `Config.Benches`.

## Gemas

`Config.Gems.provider`:

| Provider | Quando usar |
|---|---|
| `'auto'` | Usa a gema da base quando ela existe (Creative e Creative v4/v5). Sem gemas na base, a opção some. |
| `'item'` | A gema é um item do inventário (`item = 'gem'`). |
| `'custom'` | Ligue ao seu sistema de moedas/doação com três funções. |
| `'none'` | Sem gemas. |

```lua
Config.Gems = {
	provider = 'custom',
	custom = {
		get = function(src) return exports.minha_loja:GetCoins(src) end,
		remove = function(src, amount, reason) return exports.minha_loja:RemoveCoins(src, amount) end,
		add = function(src, amount, reason) return exports.minha_loja:AddCoins(src, amount) end
	}
}
```

`remove` precisa devolver `true` só quando tirou (com saldo). `add` é usado para devolver em caso de falha.

## Comissão da bancada

Uma parte de cada venda em dinheiro pode ir para o emprego dono da bancada (o armeiro ganha com o movimento):

```lua
-- Config.Benches: { id = 'ammunation', ..., society = { name = 'ammunation', percent = 30 } }
Config.Society = {
	pay = function(society, amount, reason) exports.meu_banco:AddSocietyMoney(society, amount) end
}
```

Toda venda também dispara o evento de servidor `one_workshop:server:sale` com
`{ src, bench, society, amount, share, kind, label }`, para qualquer outra integração.
