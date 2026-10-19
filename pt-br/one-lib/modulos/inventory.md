---
description: Dar e consumir itens em qualquer servidor.
---

# Inventory

O mesmo código entrega e consome itens em qualquer inventário. O módulo usa, nesta ordem, o primeiro que
estiver iniciado: **one\_inventory**, **ox\_inventory**, **qb-inventory** ou o inventário nativo do framework
(vRP Creative, Creative v5, vRPex, ESX, QBCore).

| Função | Retorno |
|---|---|
| `One.Inventory.Add(src, item, count, metadata?)` | quantidade entregue |
| `One.Inventory.Remove(src, item, count)` | `true` se removeu tudo |
| `One.Inventory.Count(src, item)` | quantidade |
| `One.Inventory.Has(src, item, count?)` | `boolean` |
| `One.Inventory.CanCarry(src, item, count)` | `boolean` |
| `One.Inventory.Provider()` | `'one_inventory'`, `'ox_inventory'`, `'qb-inventory'`, `'native'` ou `nil` |

```lua
if not One.Inventory.CanCarry(src, 'lockpick', 1) then
    return One.Notify(src, 'Sem espaço', 'error')
end

if One.Inventory.Remove(src, 'scrap', 3) then
    One.Inventory.Add(src, 'lockpick', 1)
end
```

{% hint style="info" %}
Metadados (`metadata`) só são guardados nos inventários que os suportam (one\_inventory, ox, qb). No vRP e no
ESX sem ox, o item é entregue sem eles.
{% endhint %}
