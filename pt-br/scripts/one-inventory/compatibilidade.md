---
description: Scripts feitos para ox_inventory e qb-inventory funcionam sem alteração; migração dos dados.
---

# Compatibilidade e migração

## Scripts de outros inventários

O one\_inventory responde aos exports dos inventários mais usados do mercado. Scripts escritos para eles
funcionam sem alteração:

| Camada | Liga automaticamente em | Cobre |
|---|---|---|
| `ox_inventory` | **Qbox** e **ESX** | `AddItem`, `RemoveItem`, `Search`, `GetItemCount`, `CanCarryItem`, `GetSlot*`, `SetMetadata`, `RegisterStash`, `forceOpenInventory`, `registerHook`, `CustomDrop`, `ConfiscateInventory` e os exports de cliente (`openInventory`, `Search`, `GetPlayerItems`...) |
| `qb-inventory` | **QBCore** | `AddItem`, `RemoveItem`, `HasItem`, `GetItemByName`, `CanAddItem`, `SetItemData`, `OpenInventory`, `CreateShop`/`OpenShop`... e o `PlayerData.items` do QBCore fica sempre em dia |

No **vRP / Creative / Creative v4-v5 / vRPex**, a ponte do `vrp` faz o mesmo papel com as funções de item do
core (`GiveItem`, `giveInventoryItem`, `tryGetInventoryItem`, `getInventory`...). Ver o guia da sua base em
[Instalação](instalacao/README.md).

Itens usáveis registrados no framework continuam funcionando: `QBCore.Functions.CreateUseableItem`,
`exports.qbx_core:CreateUseableItem`, `ESX.RegisterUsableItem`, as escolhas de uso do vRP 1
(`vRP.defInventoryItem`) e o uso de itens do Creative e do Creative v4/v5 (importado da base).

## Por base

| Base | Como os outros scripts chegam ao inventário | Itens usáveis |
|---|---|---|
| vRP Creative | ponte no `vrp` (`vRP.GiveItem`...) | gameplay da base importado (`oneinv_import`) |
| Creative v4/v5 | ponte no `vrp` (`vRP.giveInventoryItem`...) | `vrp_inventory` da base importado (`oneinv_import`) |
| vRPex / vRP 1 | ponte no `vrp` | escolhas do menu do vRP (`defInventoryItem`) |
| ESX Legacy | `xPlayer.*InventoryItem` no modo ox → camada `ox_inventory` | `ESX.RegisterUsableItem` |
| QBCore | `Player.Functions.AddItem` → camada `qb-inventory` | `QBCore.Functions.CreateUseableItem` |
| Qbox | `qbx_core` → camada `ox_inventory` | `exports.qbx_core:CreateUseableItem` |
| Standalone | `exports.one_inventory` | `RegisterUsable` / `consume` |

## Mira (ALT): target da base

| Base tem | Quem cuida da mira | Opções do one\_inventory (porta-malas) |
|---|---|---|
| `ox_target` | o ox\_target | aparecem dentro do ox\_target |
| `qb-target` | o qb-target | aparecem dentro do qb-target |
| `target` do Creative | o one\_lib (substitui o target; ver [Interact](../../one-lib/modulos/interact.md)) | no cartão do one\_lib |
| nenhum | o one\_lib | no cartão do one\_lib |

Marcas por proximidade (lojas, bancadas, baús) são sempre do one\_lib.

{% hint style="warning" %}
**Desligue o inventário antigo** (tire do `server.cfg`). Com o original iniciado, a camada não liga, para não
existirem dois inventários respondendo. Mantenha a pasta do `ox_inventory` no servidor: os itens são lidos de
`ox_inventory/data/items.lua` e `data/weapons.lua`.
{% endhint %}

Para forçar ou desligar uma camada:

```lua
Config.Compat = { ox = 'auto', qb = 'auto' }   -- true / false / 'auto'
```

## Migração dos dados

### ox\_inventory e qb-inventory

No console do servidor, com o one\_inventory iniciado:

```
oneinv_migrate ox
oneinv_migrate qb
```

Copia inventários de jogadores, baús, porta-malas e porta-luvas para o one\_inventory. A origem **não é apagada**
e nenhum inventário já existente no one\_inventory é sobrescrito (use `oneinv_migrate ox force` para sobrescrever).
Depois, reinicie o one\_inventory.

### vRP Creative

Não há comando: cada inventário é trazido **sozinho** na primeira vez que é usado (bolsos na primeira entrada do
personagem; baús, casas, armazéns e porta-malas na primeira abertura). O conteúdo sai do armazenamento antigo ao
entrar no novo, então não há como duplicar.

## Imagens dos itens

No Creative, as imagens de `vrp/config/inventory` são usadas automaticamente. Nas outras bases, copie os PNG do
inventário antigo para `one_inventory/web/images`:

| Inventário antigo | Pasta das imagens |
|---|---|
| ox\_inventory | `ox_inventory/web/images` |
| qb-inventory, ps-inventory, lj-inventory | `<recurso>/html/images` |
| vrp\_inventory (Creative v4/v5) | `vrp_inventory/web-side/images` |
| esx\_inventoryhud | `esx_inventoryhud/html/img/items` |

Depois, `refresh` e reinicie. `oneinv_images` no console lista os itens que ainda estão sem imagem.
Para usar outra pasta, defina `Config.ImagePath` (ex.: `'https://cdn.seusite.com/items/%s.png'`).
