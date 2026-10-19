---
description: Exports, hooks e eventos para outros scripts.
---

# Integração com outros scripts

## Alvo (`target`)

Todas as funções de servidor recebem um alvo:

| Valor | Inventário |
|---|---|
| `source` (número) | bolsos do jogador; consultas e remoções incluem a mochila |
| `'player:<charId>'` | bolsos de um personagem, mesmo offline |
| outro texto | inventário carregado (`'stash:police'`, `'trunk:ABC123'`) |

## Exports de servidor

```lua
local inv = exports.one_inventory

inv:AddItem(source, 'water', 2)                 -- → quantos entraram (não cria o que não cabe)
inv:RemoveItem(source, 'water', 1)              -- → quantos saíram
inv:GetItemCount(source, 'water')
inv:HasItem(source, 'lockpick', 1)
inv:CanCarry(source, 'scrap', 50)
inv:Search(source, 'WEAPON_PISTOL')             -- → { { slot, name, count, metadata, inventory } }
inv:GetSlot(source, 3)
inv:SetMetadata(source, 3, { label = 'Carta de Ana' })
inv:GetInventory(source)
inv:ClearInventory(source, { identity = true }) -- mantém os itens da lista

inv:OpenInventory(source, { type = 'stash', id = 'police_locker' })
inv:OpenInventory(source, { type = 'player', target = alvo }, true)   -- true = ignora as regras (admin)
inv:CloseInventory(source)

inv:RegisterStash('gang_ballas', { label = 'Ballas', slots = 80, weight = 300.0, groups = { ballas = 0 } })
inv:RegisterShop('burgershot', { label = 'Burger Shot', currency = 'money', items = { { name = 'burger', price = 12 } } })
inv:OpenShop(source, 'burgershot')       -- seu script já validou (ex.: atendente no balcão)
inv:RegisterBench('kitchen', { label = 'Cozinha', recipes = { { item = 'burger', time = 5, ingredients = { bread = 1, meat = 1 } } } })
inv:OpenBench(source, 'kitchen')
inv:CreateInventory({ id = 'house:12', label = 'Casa 12', slots = 40, weight = 150.0 })
inv:CreateDrop(coords, { { name = 'scrap', count = 5 } })
inv:RegisterItem('ticket', { label = 'Ingresso', weight = 0.01, stack = 10 })
inv:RefreshWeight(source)
inv:GetCurrentWeapon(source)
```

### Uso de item

```lua
exports.one_inventory:RegisterUsable('radio', function(source, item, slot, inventoryId)
    TriggerClientEvent('radio:open', source)
    -- retorne false para indicar que não usou
end)
```

### Hooks (podem cancelar)

```lua
exports.one_inventory:RegisterHook('beforeMove', function(payload)
    -- payload: source, from, to, fromSlot, toSlot, count, item = { name, count, metadata }
    if payload.item.name == 'WEAPON_PISTOL' and payload.to:find('^drop:') then
        return false -- não pode soltar armas
    end
end)
```

Eventos de hook: `beforeMove`, `beforeUse`, `beforeGive`, `beforeDrop`.

## Eventos de servidor

| Evento | Argumentos |
|---|---|
| `one_inventory:server:changed` | `inventoryId, owner` |
| `one_inventory:server:itemUsed` | `source, item, slot` |
| `one_inventory:server:opened` / `closed` | `source, secondaryId` |
| `one_inventory:server:playerReady` | `source, charId` |

## Exports de cliente

```lua
exports.one_inventory:OpenStash('police_locker')
exports.one_inventory:SearchPlayer(serverId)
exports.one_inventory:CloseInventory()
exports.one_inventory:IsOpen()
exports.one_inventory:GetItemCount('water')   -- leitura local, sem ida ao servidor
exports.one_inventory:HasItem('lockpick')
exports.one_inventory:GetCurrentWeapon()
```
