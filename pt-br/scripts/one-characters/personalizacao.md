---
description: Hooks abertos para adaptar o one_characters às regras do seu servidor.
---

# Personalização

Os arquivos `server/open.lua` e `client/open.lua` não são protegidos. Eles têm funções chamadas pelo
produto em momentos específicos, e você pode alterá-las à vontade.

{% hint style="info" %}
Erros dentro dos hooks não travam a seleção: eles aparecem no console e o produto usa o comportamento padrão.
{% endhint %}

## Slots

```lua
-- server/open.lua
function Hooks.GetSlots(src, frameworkSlots)
    return frameworkSlots or Config.Slots.Default
end
```

`frameworkSlots` é o que o framework informa (Creative: `accounts.Characters` + Premium; ESX:
`multicharacter_slots`), ou `nil`. Exemplo: um slot extra para quem tem permissão ACE de VIP:

```lua
function Hooks.GetSlots(src, frameworkSlots)
    local slots = frameworkSlots or Config.Slots.Default
    if IsPlayerAceAllowed(src, 'vip') then
        slots = slots + 1
    end
    return slots
end
```

## Spawns extras

```lua
-- server/open.lua
function Hooks.GetSpawns(src, charId)
    return {}
end
```

Retorne uma lista de locais exclusivos daquele personagem. Eles aparecem entre a última localização e os
spawns públicos.

| Campo | Descrição |
|---|---|
| `id` | único, ex.: `'house:12'` |
| `icon` | `home`, `bed`, `pin` ou `star` |
| `label` | texto exibido |
| `sub` | opcional; sem ele, o nome da rua é usado |
| `coords` | `vec4(x, y, z, heading)` |

Exemplo com uma tabela de casas própria:

```lua
function Hooks.GetSpawns(src, charId)
    local rows = One.DB.Query('SELECT id, label, x, y, z FROM houses WHERE owner = ?', { charId })
    local spawns = {}
    for _, house in ipairs(rows or {}) do
        spawns[#spawns + 1] = {
            id = 'house:' .. house.id,
            icon = 'home',
            label = house.label,
            coords = vec4(house.x, house.y, house.z, 0.0)
        }
    end
    return spawns
end
```

{% hint style="success" %}
No **vRP Creative** as propriedades do script `propertys` já aparecem automaticamente (ou o hotel, para
quem não tem casa).
{% endhint %}

## Personagem criado

```lua
-- server/open.lua
function Hooks.OnCreated(src, charId, identity)
end
```

Chamado depois que o personagem foi criado e entrou na cidade. `identity` tem `firstName`, `lastName`,
`dob`, `sex`, `nationality` e `bio`. Use para itens iniciais, mensagem de boas-vindas, log etc.

{% hint style="info" %}
Os itens iniciais do próprio framework (Creative, QBCore `StarterItems`, Qbox `starterItems`) já são
entregues automaticamente.
{% endhint %}

## Ao aparecer na cidade

```lua
-- client/open.lua
function Hooks.OnSpawned(isNew)
end
```

Chamado no fim da transição. Os eventos que o seu framework espera (HUD do Creative, `esx:onPlayerSpawn`,
`QBCore:Client:OnPlayerLoaded`) já foram disparados antes deste hook.

## Textos

Todos os textos ficam em `locales/pt-BR.lua` e `locales/en.lua`, inclusive os da interface. Mude o que
quiser. As chaves com `{nome}` recebem valores dinâmicos:

```lua
['select.online'] = '{count} na cidade',
```

## Cena própria

Mova `Config.Scene.Lineup` e `Config.Scene.Creator` para um mapa seu (um apartamento, um terraço, uma
garagem). Use as coordenadas do **chão**. A câmera se ajusta às paredes sozinha.
