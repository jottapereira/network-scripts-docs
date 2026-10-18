---
description: Limite de frequência por jogador e por ação.
---

# RateLimit

```lua
if not One.RateLimit.Check(src, 'garage:spawn', 2, 5000) then
    return One.Notify(src, 'Aguarde um instante', 'warning')
end
```

| Função | Descrição |
|---|---|
| `One.RateLimit.Check(src, key, max, windowMs)` | `true` se permitido (e contabiliza), `false` se o limite estourou |
| `One.RateLimit.Reset(src, key?)` | zera um limite, ou todos do jogador |

Os contadores de um jogador são limpos quando ele sai. Callbacks registrados com
[`One.Callback`](callback.md) já usam este módulo automaticamente.
