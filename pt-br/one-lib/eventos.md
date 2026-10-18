---
description: Eventos normalizados do one_lib, iguais em todos os frameworks.
---

# Eventos

| Evento | Lado | Argumentos | Quando |
|---|---|---|---|
| `one:server:playerLoaded` | servidor | `src, charId` | um personagem foi carregado |
| `one:server:playerUnloaded` | servidor | `src, charId` | o personagem saiu (desconexão ou troca) |
| `one:client:playerLoaded` | cliente | `charId` | o personagem local foi carregado |
| `one:client:playerUnloaded` | cliente | `charId` | o personagem local saiu |
| `one:server:log` | servidor | `{ channel, resource, source, name, charId, message, data }` | um produto registrou exploit ou auditoria |

```lua
AddEventHandler('one:server:playerLoaded', function(src, charId)
    -- funciona em Creative, ESX, QBCore, Qbox e Standalone
end)
```

{% hint style="info" %}
São eventos **locais** (`AddEventHandler`): clientes não conseguem dispará-los no servidor.
Prefira [`One.Player.OnLoaded`](modulos/player.md), que também avisa sobre quem já está online.
{% endhint %}

## Integrando seu sistema de logs

```lua
AddEventHandler('one:server:log', function(entry)
    -- entry.channel = 'exploit', 'characters', 'audit'...
    -- envie para o seu sistema de logs
end)
```
