---
description: ESX Legacy, com ou sem ox_inventory. Cerca de 10 minutos.
---

# Instalação: ESX Legacy

O ESX Legacy entrega os itens para o inventário pelo "modo ox": `xPlayer.addInventoryItem`, `removeInventoryItem`,
`getInventoryItem` e companhia chamam `exports.ox_inventory`. O one\_inventory **responde por esses exports**,
então o ESX e os scripts feitos para ox\_inventory passam a usar o inventário novo sem alteração.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure es_extended

ensure one_lib
ensure one_inventory

# depois: os demais scripts (esx_*, ox_target...)
```
{% endstep %}

{% step %}
### Desligue o ox\_inventory (mantenha a pasta)

Tire `ensure ox_inventory` do `server.cfg`, mas **deixe a pasta `ox_inventory` no servidor**:

* o ESX só usa o "modo ox" quando encontra a pasta (`Config.OxInventory`);
* a lista de itens é lida de `ox_inventory/data/items.lua` e `data/weapons.lua`.

O one\_inventory se declara `ox_inventory` (`provide`), então scripts com `dependency 'ox_inventory'` iniciam
normalmente.
{% endstep %}

{% step %}
### Sua base não usava ox\_inventory?

Bases ESX com o inventário padrão (`esx_inventory`, `esx_inventoryhud`): **tire o `ensure` deles** (mantenha as
pastas). Os itens vêm da tabela `items` do banco (nome, label e peso).

* **ESX 1.16 ou mais novo:** nada a configurar. O ESX encontra o `ox_inventory` (que é o one\_inventory) e liga o
  modo ox sozinho.
* **ESX mais antigo:** ligue o modo ox no `es_extended/config.lua`: `Config.OxInventory = true`.

No modo ox o **dinheiro em espécie e o sujo são itens** (`money` e `black_money`), como no ox\_inventory. Na
primeira entrada de cada personagem, os itens e o dinheiro que ele tinha no ESX passam para o inventário.
{% endstep %}

{% step %}
### Migre os inventários (vindo do ox\_inventory)

No console do servidor:

```
oneinv_migrate ox
```

Copia jogadores, baús, porta-malas e porta-luvas. A origem não é apagada. Depois, reinicie o one\_inventory.
{% endstep %}

{% step %}
### Imagens

Copie `ox_inventory/web/images/` para `one_inventory/web/images/` (ou a pasta de imagens do seu inventário).
`refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_inventory] 380 itens registrados (esx)
[one_inventory] compatibilidade ox_inventory ativa
```

No jogo: `TAB` abre o inventário; um script que dá item pelo `xPlayer.addInventoryItem` entrega no one\_inventory.

## Observações

* **Itens usáveis** (`ESX.RegisterUsableItem`) continuam funcionando ao usar o item.
* **Dinheiro:** `money` (carteira), `bank` e `black_money` são contas do ESX; lojas cobram com
  `currency = 'cash' | 'bank' | 'dirty'`.
* **ox\_target:** se a base usa, a mira (ALT) continua sendo dele; as opções do one\_inventory (porta-malas)
  aparecem dentro do ox\_target. As marcas de loja, bancada e baú aparecem ao chegar perto.
* **Sistema de roupa** (acessórios como itens): `illenium-appearance`, `fivem-appearance` ou `skinchanger`.
