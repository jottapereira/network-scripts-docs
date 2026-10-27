---
description: Como as skins funcionam, como gerar o pacote do seu servidor e como vender.
---

# Skins

## Como funciona

Cada skin é um **componente da arma** (o mesmo tipo do "acabamento de luxo" do GTA). Ela troca o modelo inteiro da
arma, mas a arma continua sendo `WEAPON_X`:

* inventário, munição e acessórios continuam iguais;
* os outros jogadores veem a skin sem nada extra (o jogo sincroniza o componente);
* trocar de skin é instantâneo na bancada.

O jogador vê as skins da arma que está na mão na aba **Skins** da bancada: passa o mouse para ver na arma da mesa,
clica para equipar e compra pela forma de pagamento que preferir. Comprou, é dele: serve em qualquer arma daquele
modelo, e trocar é grátis.

## O pacote de skins

As skins ficam em **pacotes**: recursos separados com os modelos, as texturas e um `skins.json`. Você pode ligar vários pacotes
(o da Network One, de outros criadores, os seus). Como ligar, o formato e as opções por pacote: [Pacotes de skins](pacotes.md).

{% hint style="warning" %}
O pacote da Network One é gerado a partir dos arquivos do GTA, no **seu** computador, com o seu jogo. Esse material não é
distribuído por nós.
{% endhint %}

Depois de ligar os pacotes (`ensure` antes da oficina), reinicie o servidor e peça para os jogadores **reconectarem**.
`workshop_skins` no console mostra o que a oficina encontrou.

## Raridade e preço

Cada estilo tem uma raridade (`Config.Skins.tier`): comum, rara, épica ou lendária. O preço padrão vem da raridade
(`Config.Skins.prices`) e pode ser ajustado:

```lua
Config.Skins.prices = {
	common = { cash = 15000, gems = 60, items = { wk_skin_token = 1 } },
	rare = { cash = 40000, gems = 160, items = { wk_skin_token = 2 } },
	epic = { cash = 90000, gems = 360, items = { wk_skin_token = 4 } },
	legendary = { cash = 200000, gems = 800, items = { wk_skin_token = 8 } }
}
Config.Skins.factor = { WEAPON_HEAVYSNIPER = 1.5 }          -- arma mais cara
Config.Skins.override = { dragao = { gems = 1200 } }         -- só gemas, preço próprio
Config.Skins.starter = { 'ouro' }                            -- todo mundo ganha
```

Quais formas o jogador pode usar (dinheiro, itens, gemas) depende de `Config.Pricing.skins`. Veja
[Cobrança](cobranca.md).

## Skins exclusivas

Restrinja por estilo ou por componente com `Config.Skins.access`. Sem acesso, o cartão aparece trancado:

```lua
Config.Skins.access = {
	dragao = { groups = { 'vip' } },                     -- VIP
	hexa = { groups = { 'police' }, grade = 2 },          -- polícia, cargo 2 ou mais
	COMPONENT_PISTOL_SKIN_V1_OURO = { ace = 'skins.ouro' } -- permissão ACE
}
```

Para entregar uma skin sem cobrar (evento, doação, recompensa), use `/oficina_dar` (veja
[Administração](administracao.md)).
