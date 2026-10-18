---
description: Eventos e comportamento para integrar outros scripts com o one_characters.
---

# Integração com outros scripts

## Eventos

| Evento | Lado | Argumentos | Quando |
|---|---|---|---|
| `one_characters:server:created` | servidor | `src, charId` | personagem novo criado e já dentro da cidade |
| `one_characters:client:spawned` | cliente | `isNew` | fim da transição de entrada |

```lua
-- servidor: dar um carro para todo personagem novo
AddEventHandler('one_characters:server:created', function(src, charId)
    -- seu código
end)
```

Para saber quando **qualquer** personagem entra ou sai, use os eventos do `one_lib`, que funcionam em
todos os frameworks: `one:server:playerLoaded` e `one:server:playerUnloaded`. Veja [Eventos](../../one-lib/eventos.md).

## Eventos do framework

O produto dispara, no spawn, os mesmos eventos que o sistema original do framework disparava. Scripts que
dependem deles continuam funcionando sem mudança:

| Framework | Disparado ao entrar na cidade |
|---|---|
| vRP Creative | `hud:Active` |
| ESX | `esx:onPlayerSpawn` (cliente e servidor), `esx:restoreLoadout`, e na abertura `esx:loadingScreenOff` |
| QBCore / Qbox | `QBCore:Server:OnPlayerLoaded`, `QBCore:Client:OnPlayerLoaded` |

## Aparência

A aparência criada é gravada no sistema de roupa do servidor (veja
[Frameworks suportados](../../comece-aqui/frameworks-suportados.md#sistemas-de-roupa)). Barbearias, lojas
e outfits passam a ver o personagem criado normalmente.

## Privacidade da seleção

Durante a seleção e a criação, cada jogador fica num *routing bucket* próprio (`Config.Scene.BucketBase` +
id do jogador): ninguém vê ninguém. Ao entrar na cidade, ele volta ao bucket `0`.
