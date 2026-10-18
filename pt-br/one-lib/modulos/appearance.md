---
description: Aparência em um formato único, salva no sistema de roupa do servidor.
---

# Appearance

## Formato

```lua
{
    model = 'mp_m_freemode_01',
    heritage = { shapeFirst = 0, shapeSecond = 21, skinFirst = 0, skinSecond = 21, shapeMix = 0.5, skinMix = 0.5 },
    face = { 0.0, 0.0, ... },              -- 20 valores de -1 a 1 (face[i + 1] = feature nativa i)
    eyes = 0,
    hair = { style = 4, texture = 0, color = 3, highlight = 3 },
    overlays = { beard = { style = 10, opacity = 0.8, color = 3, secondColor = 3 } },   -- style -1 = nenhum
    components = { torso = { drawable = 273, texture = 0 } },
    props = { hat = { drawable = -1, texture = 0 } }                                    -- -1 = nenhum
}
```

| Grupo | Nomes |
|---|---|
| `components` | `mask` `arms` `pants` `bag` `shoes` `accessory` `undershirt` `armor` `decals` `torso` |
| `props` | `hat` `glasses` `ears` `watch` `bracelet` |
| `overlays` | `blemishes` `beard` `eyebrows` `ageing` `makeup` `blush` `complexion` `sundamage` `lipstick` `moles` `chesthair` `bodyblemishes` |

## Todos os lados

| Função | Descrição |
|---|---|
| `One.Appearance.Default(model)` | aparência base |
| `One.Appearance.Sanitize(data)` | valida aparência vinda do cliente. Retorna a versão limpa ou `nil, campo` |
| `One.Appearance.IsFreemode(model)` | `true` para os modelos de personagem online |

## Cliente

| Função | Descrição |
|---|---|
| `SetPlayerModel(model)` | troca o modelo do jogador e retorna o novo ped |
| `Apply(ped, data)` | aplica tudo (também `ApplyHeritage`, `ApplyFace`, `ApplyHair`, `ApplyOverlay`, `ApplyComponent`, `ApplyProp`) |
| `Headshot(ped, transparent?)` | retrato para a NUI: `handle, url`. Chame `UnregisterPedheadshot(handle)` depois |
| `GetLimits(ped)` | quantidade real de modelos de cada peça, para a UI não oferecer o que não existe |

## Servidor

| Função | Descrição |
|---|---|
| `Get(charId)` / `GetMany(charIds)` | lê do sistema de roupa do servidor |
| `Save(charId, data)` | grava no sistema de roupa (use `Sanitize` antes) |
| `Capabilities.skinMix` | `false` quando o sistema só guarda o tom de pele de um dos pais (Creative) |
| `system` | sistema detectado: `creative`, `illenium`, `skinchanger` ou `one` |

```lua
local appearance = One.Appearance.Sanitize(dataFromClient)
if not appearance then return end
One.Appearance.Save(charId, appearance)
```
