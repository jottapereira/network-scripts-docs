---
description: Identidade do personagem e ciclo de vida, igual em todos os frameworks.
---

# Player

O `charId` é sempre uma **string**, seja um Passport, um identifier ou um citizenid.

## Servidor

| Função | Retorno |
|---|---|
| `One.Player.GetCharId(src)` | `charId` ou `nil` |
| `One.Player.GetSource(charId)` | `source` ou `nil` |
| `One.Player.IsLoaded(src)` | `boolean` |
| `One.Player.GetName(src)` | nome do personagem |
| `One.Player.GetAll()` | `{ [source] = charId }` (somente leitura) |
| `One.Player.OnLoaded(cb)` | `cb(src, charId)` ao carregar um personagem |
| `One.Player.OnUnloaded(cb)` | `cb(src, charId)` ao sair do personagem |

{% hint style="info" %}
`OnLoaded` também chama `cb` para quem **já está** online. Seu script funciona igual se for reiniciado com o
servidor cheio.
{% endhint %}

```lua
One.Player.OnLoaded(function(src, charId)
    print(('%s entrou como %s'):format(GetPlayerName(src), One.Player.GetName(src)))
end)
```

## Cliente

| Função | Retorno |
|---|---|
| `One.Player.GetCharId()` | `charId` do jogador local ou `nil` |
| `One.Player.IsLoaded()` | `boolean` |
| `One.Player.OnLoaded(cb)` | `cb(charId)`, também chamada na hora se já estiver carregado |
| `One.Player.OnUnloaded(cb)` | `cb(charId)` |

Todas as consultas leem uma tabela local: custo zero, mesmo em loops.
