---
description: Todas as opções do config.lua do one_characters.
---

# Configuração

## Geral

| Opção | Padrão | Descrição |
|---|---|---|
| `Config.Locale` | `nil` | idioma deste produto. `nil` usa o idioma global (`setr one:locale`) |
| `Config.Sounds` | `true` | sons de interface (sons nativos dos menus do GTA) |
| `Config.AllowDelete` | `true` | permite que o jogador exclua personagens. Com `false`, o botão some |

## Marca

```lua
Config.Branding = {
    Mark = 'N1',                       -- sigla no quadrado do canto
    Name = 'NETWORK ONE',              -- nome da cidade
    Subtitle = 'Roleplay · Temporada 1'
}
```

## Slots

```lua
Config.Slots = {
    Display = 4,   -- quantos cards aparecem (os acima do limite da conta aparecem bloqueados)
    Default = 2    -- usado quando o framework não define slots
}
```

{% hint style="info" %}
Slots acima do limite da conta aparecem como **"Disponível para apoiadores"**. Para dar slots por cargo,
VIP ou qualquer regra, use [`Hooks.GetSlots`](personalizacao.md#slots).
{% endhint %}

## Identidade

```lua
Config.Identity = {
    NameMin = 2,
    NameMax = 16,
    BlockedNames = { 'admin', 'staff', 'moderador', 'policia', 'police', 'suporte' },
    AgeMin = 18,
    AgeMax = 90,
    BioMax = 240,
    Nationalities = { 'Estados Unidos', 'Brasil', 'México', '...', 'Outro' }
}
```

| Opção | Descrição |
|---|---|
| `NameMin` / `NameMax` | tamanho do nome e do sobrenome. Aceita letras com acento, espaço, hífen e apóstrofo |
| `BlockedNames` | trechos proibidos no nome completo, sem diferenciar maiúsculas |
| `AgeMin` / `AgeMax` | idade permitida, calculada pela data de nascimento |
| `BioMax` | tamanho máximo da história |
| `Nationalities` | lista exibida no criador. O servidor só aceita valores desta lista |

## Cena

```lua
Config.Scene = {
    Lineup = vec4(402.9, -996.6, -100.0, 180.0),   -- centro do line-up (z = chão, w = direção)
    Spacing = 1.0,                                 -- distância entre personagens
    MaxVisible = 4,                                -- personagens visíveis ao mesmo tempo
    Creator = vec4(402.9, -996.6, -100.0, 180.0),  -- onde fica o personagem durante a criação
    BucketBase = 20000,                            -- buckets privados: BucketBase + id do jogador
    Idles = { m = { ... }, f = { ... } }           -- animações sorteadas no line-up
}
```

A cena padrão é a sala de line-up do criador do GTA Online: um interior sempre vazio e com luz controlada.
Você pode mover para qualquer lugar do mapa. A câmera detecta paredes e se ajusta sozinha.

{% hint style="warning" %}
`z` é a **altura do chão**, não a altura do personagem. Use as coordenadas do chão onde ele vai pisar.
{% endhint %}

## Spawns

```lua
Config.StartSpawn = vec4(-1039.47, -2739.57, 13.85, 330.0)   -- onde nasce o personagem recém-criado

Config.Spawns = {
    { id = 'airport',  icon = 'star', label = 'spawn.airport',  coords = vec4(-1040.43, -2742.4, 13.92, 330.0) },
    { id = 'downtown', icon = 'star', label = 'spawn.downtown', coords = vec4(-206.9, -1015.09, 30.13, 70.0) },
}
```

| Campo | Descrição |
|---|---|
| `id` | identificador único (não exibido) |
| `icon` | `pin`, `home`, `bed` ou `star` |
| `label` | **chave de idioma** em `locales/*.lua` (ex.: `spawn.airport`) |
| `coords` | posição e direção. O nome da rua aparece automaticamente na interface |

A **última localização** do personagem sempre aparece em primeiro, quando existe. Spawns por
personagem (casas, base da facção) entram por [`Hooks.GetSpawns`](personalizacao.md#spawns-extras).

## Aparência inicial

Roupa e cabelo com que o criador começa, por sexo:

```lua
Config.DefaultAppearance = {
    m = {
        hair = { style = 4, texture = 0, color = 3, highlight = 3 },
        overlays = {
            eyebrows = { style = 1, opacity = 1.0, color = 3 },
            beard = { style = 10, opacity = 0.8, color = 3 }
        },
        components = {
            torso = { drawable = 273, texture = 0 },
            undershirt = { drawable = 15, texture = 0 },
            arms = { drawable = 0, texture = 0 },
            pants = { drawable = 4, texture = 1 },
            shoes = { drawable = 1, texture = 6 }
        },
        props = {}
    },
    f = { ... }
}
```

Peças disponíveis: `mask`, `arms`, `pants`, `bag`, `shoes`, `accessory`, `undershirt`, `armor`, `decals`,
`torso`. Acessórios (`props`): `hat`, `glasses`, `ears`, `watch`, `bracelet` (`drawable = -1` = nenhum).

## shared/data.lua

| Tabela | Para quê |
|---|---|
| `Data.Fathers` · `Data.Mothers` | pais disponíveis na herança (ids nativos do GTA) |
| `Data.EyeColors` | cores de olho exibidas, na ordem dos índices do jogo |
| `Data.FaceInvert` | features de rosto com sinal invertido, para que "direita = mais" em todos os sliders |
