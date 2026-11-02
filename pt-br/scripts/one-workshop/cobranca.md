---
description: "Como a oficina cobra acessórios, cores e skins: regras por forma de pagar, só nesta arma ou vitalício, por tipo de bancada, e como ligar as gemas do seu servidor."
---

# Cobrança: regras, escopo e tipos de bancada

## Regras de cobrança

Cada categoria (**parts** = acessórios e acabamentos do jogo, **paint** = cor da arma, **skins** = pacote de skins) é uma
**lista de regras**. Cada regra é uma forma de pagar que o jogador pode escolher:

| Campo | Valores | O que faz |
|---|---|---|
| `pay` | `'item'`, `'money'`, `'gems'` | Itens (acessórios: `Config.Items`; cor: `Config.PaintItem`; skins: os `items` do preço), dinheiro (contas de `accounts`, na ordem) ou gemas. |
| `scope` | `'weapon'`, `'lifetime'` | **weapon**: vale só para esta arma e fica gravado no item dela. **lifetime**: o personagem desbloqueia para sempre e usa em qualquer arma do mesmo modelo. Sem `scope`: acessórios e cor = weapon, skins = lifetime. A cor não desbloqueia nada: é sempre weapon. |
| `factor` | número | Multiplica o preço base (dinheiro, gemas e quantidade de itens). |
| `cash`, `gems`, `items` | valor | Preço fixo no lugar do preço base. |

A mesma forma pode aparecer duas vezes com escopos diferentes: dinheiro **só nesta arma** (barato) e dinheiro **vitalício** (caro).

```lua
Config.Pricing = {
	accounts = { 'cash', 'bank' },
	parts = {
		{ pay = 'item',  scope = 'weapon' },                  -- item: fica só nesta arma
		{ pay = 'money', scope = 'weapon' },                  -- dinheiro, preço base: só nesta arma
		{ pay = 'money', scope = 'lifetime', factor = 6 },    -- dinheiro, 6x o preço: vitalício
		{ pay = 'gems',  scope = 'lifetime' }                 -- gemas: vitalício
	},
	paint = { { pay = 'item' }, { pay = 'money' } },
	skins = {
		{ pay = 'item',  scope = 'weapon' },
		{ pay = 'money', scope = 'weapon', factor = 0.25 },
		{ pay = 'money', scope = 'lifetime' },
		{ pay = 'gems',  scope = 'lifetime' }
	}
}
```

`false` deixa a categoria grátis. As formas antigas em texto (`'item'`, `'money'`, `'gems'`, `'hybrid'`, `'free'`) continuam valendo.

### O que o jogador vê

Na bancada, o **Aplicar** cobra tudo de uma vez. A barra de baixo tem uma linha por categoria (acessórios, skin, cor), com
cada forma de pagar e o escopo ("só nesta arma" ou "vitalício"); o jogador clica na que quer.

* Itens que saem da arma (instalados com item, só nesta arma) voltam ao inventário. Dinheiro e gemas não voltam.
* Quem já desbloqueou um componente para sempre encaixa de graça, em qualquer arma do mesmo modelo.
* Uma peça paga "só nesta arma" fica gravada na arma: se a arma muda de dono, a peça vai junto.
* A cobrança é feita no servidor e é tudo-ou-nada: se algo falhar no meio, o que já saiu volta.

## Cada tipo de bancada cobra do seu jeito

Em `Config.BenchTypes`, cada tipo pode ter o seu `pricing`; o que ele não define usa `Config.Pricing`. Crie quantos tipos quiser:

```lua
Config.BenchTypes = {
	-- Ammu-Nation: acessórios só por dinheiro (nesta arma ou vitalício)
	ammunation = { parts = true, paint = true, skins = true, pricing = {
		parts = { { pay = 'money', scope = 'weapon' }, { pay = 'money', scope = 'lifetime', factor = 6 } },
		paint = { { pay = 'money' } }
	} },

	-- Arsenal da polícia: acessórios e cor de graça, só para a polícia
	police = { parts = true, paint = true, skins = true, groups = { 'police' }, pricing = { parts = false, paint = false } },

	-- Clandestina: tudo por itens; skins por item (nesta arma) ou gemas (vitalícia)
	clandestine = { parts = true, paint = true, skins = true, pricing = {
		parts = { { pay = 'item', scope = 'weapon' } },
		paint = { { pay = 'item' } },
		skins = { { pay = 'item', scope = 'weapon' }, { pay = 'gems', scope = 'lifetime' } }
	} }
}
```

Os três vêm prontos como exemplo. Para testar sem criar bancada no mapa, com `setr one_workshop:debug true` no `server.cfg`:
`/oficina ammunation`, `/oficina police`, `/oficina clandestine`.

## Preços base

Os preços abaixo são o **valor base**: as regras acima multiplicam e escolhem a forma de pagar.

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
| `'account'` | A gema é uma **conta nativa do framework**, sem item e sem script extra: no QBCore/Qbox use `account = 'crypto'` (ou um tipo novo em `MoneyTypes`); no ESX, o nome de uma conta de dinheiro sua. |
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

`remove` precisa devolver `true` só quando tirou (com saldo). `add` é usado para devolver em caso de falha. Sem fonte de gemas,
as regras com `pay = 'gems'` simplesmente não aparecem para o jogador.

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
