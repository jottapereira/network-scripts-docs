---
description: Pedir e responder dados entre cliente e servidor, com rate limit por padrão.
---

# Callback

## Cliente pergunta, servidor responde

```lua
-- servidor
One.Callback.Register('shop:buy', function(src, itemId)
    itemId = One.Utils.String(itemId, 32)
    if not itemId then return false end
    return One.Money.Pay(src, 500) ~= nil
end, { rate = { max = 3, window = 1000 } })

-- cliente
local ok = One.Callback.Await('shop:buy', 'water')
```

| Função | Lado | Descrição |
|---|---|---|
| `Register(name, handler, opts?)` | servidor | `handler(src, ...)`. `opts.rate = { max, window }` ou `false` |
| `Await(name, ...)` | cliente | chama e espera. Retorna `nil` em erro, rate limit ou timeout (15 s) |
| `Trigger(name, cb, ...)` | cliente | versão sem bloquear: `cb(...)` |

{% hint style="info" %}
Sem `opts`, todo callback já tem limite de **10 chamadas por segundo** por jogador. Use `rate = false` só
em callbacks internos e baratos.
{% endhint %}

## Servidor pergunta, cliente responde

```lua
-- cliente
One.Callback.Register('getStreet', function()
    local c = GetEntityCoords(PlayerPedId())
    return GetStreetNameFromHashKey(GetStreetNameAtCoord(c.x, c.y, c.z))
end)

-- servidor
local street = One.Callback.AwaitClient(src, 'getStreet')
```

`AwaitClient` espera até 10 s e só aceita a resposta do jogador perguntado.

{% hint style="warning" %}
Trate tudo que vem do cliente como não confiável e valide com [`One.Utils`](utils.md).
{% endhint %}
