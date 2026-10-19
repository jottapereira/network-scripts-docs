---
description: vRP Creative v4/v5 (vrp_creative, vrp_inventory). Cerca de 10 minutos.
---

# Instalação: vRP Creative v4/v5

Para bases com `vrp_inventory`, `vrp_chest`, `vrp_trunkchest` e jogadores em `vrp_users` (Creative v4, v5 e
derivadas, como a "Three").

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure vrp

ensure one_lib
ensure one_inventory

ensure [vrp]
```
{% endstep %}

{% step %}
### Ligue a ponte no vRP

No `fxmanifest.lua` (ou `__resource.lua`) do recurso `vrp`, adicione **uma linha no fim** de `server_scripts`:

```lua
server_scripts {
    -- ... o que já estava aqui ...
    '@one_inventory/bridge/vrp.lua'
}
```

`vRP.giveInventoryItem`, `tryGetInventoryItem`, `getInventoryItemAmount`, `getInventory` e o peso passam a usar
o inventário novo. Lojas (`vrp_shops`), baús (`vrp_chest`, `vrp_homes`), crafting e revista continuam funcionando
com os itens do jogador.
{% endstep %}

{% step %}
### Importe o uso dos itens

O uso dos itens (comer, bandagem, kits, pesca, recarga, placa...) fica no `vrp_inventory` da sua base. Com o
servidor ligado, rode no console:

```
oneinv_import
```

O arquivo é copiado para `one_inventory/extensions/creativev5/legacy/` e roda isolado, só para o uso de itens.
{% endstep %}

{% step %}
### Desligue o inventário antigo

Tire `vrp_inventory` do `server.cfg` (ou mova para uma pasta que não inicia), **sem apagar a pasta**.

Opcional: `vrp_trunkchest` e `vrp_chest` podem continuar (usam a interface deles). Se quiser o porta-malas e os
baús do one\_inventory, desligue-os também; o conteúdo antigo **não** é migrado automaticamente nesses dois.
{% endstep %}

{% step %}
### Imagens

Copie as imagens de `vrp_inventory/web-side/images/` (ou a pasta de imagens do seu inventário) para
`one_inventory/web/images/`. Depois, `refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_inventory] 312 itens registrados (creativev5)
[one_inventory] uso de itens da base: 87 itens ligados
[one_inventory] ponte vRP ativa
```

## Observações

* **Itens:** lidos da tabela `itemlist` de `vrp/modules/inventory.lua`: nome, peso, tipo (`use`, arma `equip`,
  munição `recharge`). Para ajustar categoria, raridade ou descrição, use `items.lua` do one\_inventory.
* **Dinheiro:** `dollars` e `dollars2` são itens; ajuste pelos convars `one:creativev5:cash_item` e
  `one:creativev5:dirty_item` se a sua base usar outros nomes.
* **Peso máximo:** padrão `Config.Player.Weight`. Se a sua base aumenta o peso por mochila/VIP, avise o suporte
  que mostramos como ligar pelo hook `GetPlayerWeight`.
