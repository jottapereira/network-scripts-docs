---
description: Moeda premium da cidade (gemas), da base, de um item ou do seu próprio sistema.
---

# Gems

A moeda que o dono do servidor vende. Cada base guarda de um jeito, então a fonte é configurável por recurso.

| Função | Retorno |
|---|---|
| `One.Gems.Configure({ provider, item?, custom? })` | configura a fonte deste recurso |
| `One.Gems.Available()` | `boolean`: há gemas nesta base/configuração |
| `One.Gems.Get(src)` | saldo ou `nil` |
| `One.Gems.Remove(src, amount, reason?)` | `boolean`. Só remove se houver saldo |
| `One.Gems.Add(src, amount, reason?)` | `boolean` |

## Fontes (`provider`)

| Valor | Quando usar |
|---|---|
| `'auto'` | usa a gema da base quando existe: Creative (`UserGemstone`, `PaymentGemstone`, `UpgradeGemstone`) e Creative v4/v5 (`userGemstone`, `paymentGems`, `upgradeGemstone`). Nas outras bases fica desligado |
| `'item'` | a gema é um item do inventário (`item = 'gem'`) |
| `'custom'` | funções suas: `get(src)`, `remove(src, amount, reason)`, `add(src, amount, reason)` |
| `'none'` | sem gemas |

```lua
One.Gems.Configure({
    provider = 'custom',
    custom = {
        get = function(src) return exports.minha_loja:GetCoins(src) end,
        remove = function(src, amount) return exports.minha_loja:RemoveCoins(src, amount) end,
        add = function(src, amount) return exports.minha_loja:AddCoins(src, amount) end
    }
})

if One.Gems.Available() and One.Gems.Remove(src, 120, 'skin') then
    -- cobrou 120 gemas
end
```

{% hint style="info" %}
Valores são sempre **inteiros positivos**. `remove` precisa devolver `true` só quando tirou de verdade (com saldo).
{% endhint %}
