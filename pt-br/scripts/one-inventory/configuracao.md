---
description: config.lua, items.lua e as regras do seu servidor.
---

# Configuração

## config.lua

| Opção | Padrão | O que faz |
|---|---|---|
| `Config.Accent` | `nil` | cor de destaque das telas deste script (`'#ff6a00'`). `nil` usa a cor geral. Ver [Cor das telas](../../comece-aqui/cor-das-telas.md) |
| `Config.OpenKey` | `TAB` | Tecla de abrir (o jogador pode trocar nas configurações do FiveM) |
| `Config.Layout` | `'open'` | `'open'`: compacto, o jogo continua visível e a câmera não mexe, acessórios numa coluna ao lado do inventário. `'classic'`: tela escurecida, cabeçalho e personagem no centro com o equipamento em volta (`Config.Preview`) |
| `Config.Player.Slots` / `Weight` / `Hotbar` | `30` / `30.0` kg / `5` | Bolsos do personagem |
| `Config.Equipment` | chapéu, óculos, máscara, colete, luvas, mochila | Slots de equipamento |
| `Config.BackpackSlots` | `20` | Slots de uma mochila que só define o peso |
| `Config.ContainerSlots` / `ContainerWeight` | `15` / `20.0` | Maletas importadas sem capacidade definida |
| `Config.Drops` | 15 min, raio 1,5 m | Itens no chão: tempo de vida, agrupamento, distância |
| `Config.Vehicles.Classes` / `Models` | por classe | Capacidade do porta-malas; modelo sobrescreve a classe |
| `Config.Vehicles.Glovebox` | 5 slots, 5 kg | Porta-luvas |
| `Config.Stashes` | vazio | Baús fixos (coordenadas, grupos, pessoal) |
| `Config.SaveInterval` | `60` s | Gravação em lote no banco |
| `Config.Weapons` | 3 s, 250 | Sincronia de munição e máximo carregado |
| `Config.Animations` | comer, beber, remédio... | Animações e objetos do consumo |
| `Config.EquipmentVisuals` | vazio | Peça de roupa aplicada ao equipar um item |

### Baú fixo

```lua
Config.Stashes = {
    { id = 'police_locker', label = 'Armário da Polícia', coords = vec3(452.0, -980.0, 30.7), radius = 2.0,
      slots = 50, weight = 200.0, groups = { police = 0 }, personal = true }
}
```

`personal = true` dá um baú por personagem. `groups` exige grupo e grau mínimo.

### Loja

```lua
Config.Shops = {
    ['247'] = {
        label = 'Loja 24/7', mode = 'buy', currency = 'money',
        locations = { vec3(24.51, -1346.75, 29.49) }, radius = 2.0,
        items = { { name = 'water', price = 6 }, { name = 'sandwich', price = 9, stock = 50 } }
    },
    ['pawn'] = {
        label = 'Penhores', mode = 'sell', currency = 'cash',
        locations = { vec3(174.99, -1323.47, 29.65) },
        items = { { name = 'goldnecklace', price = 625 } }
    }
}
```

* `mode`: `buy` (o jogador compra) ou `sell` (o jogador vende; arraste o item para a loja).
* `currency`: `cash`, `bank`, `dirty`, `money` (carteira e depois banco) ou o **nome de um item** (ex.: dinheiro sujo).
* `stock` é opcional e fica gravado; sem `stock`, é infinito.
* Cada ponto de `locations` ganha a marca de [interação](../../one-lib/modulos/interact.md): o jogador vê de
  longe, chega perto e aperta `E`. Quem não tem acesso (grupo, serviço) não vê o ponto. Sem `locations`, a loja só
  abre por script (`OpenShop`).
* Bancadas e baús com `coords` (`Config.Stashes`) funcionam do mesmo jeito. O porta-malas abre mirando no carro
  (segure `ALT`); o TAB abre o porta-luvas dentro do veículo e o chão.

### Bancada

```lua
Config.Benches = {
    workshop = {
        label = 'Bancada', locations = { vec3(949.69, -957.4, 39.83) }, groups = { mechanic = 0 },
        recipes = {
            { item = 'lockpick', count = 1, time = 4, ingredients = { scrap = 2, plastic = 1 } },
            { item = 'repairkit', count = 1, time = 8, ingredients = { scrap = 5, rubber = 2 }, level = 2 }
        }
    }
}
```

Os ingredientes saem ao entrar na fila; o item sai pronto depois do tempo. A fila continua correndo com o jogador
offline e é entregue na próxima entrada. Sem espaço, o item cai no chão ao lado.

### Peso que pesa

```lua
Config.Burden = { Enabled = true, NoSprint = 0.85, Slow = 0.95, SlowRate = 0.85 }
```

Com a carga (bolsos + mochila) acima de 85% da capacidade, o personagem não corre; acima de 95%, anda mais
devagar e não pula. Calculado quando o peso muda: sem custo enquanto a carga é normal.

### Mochilas

Uma mochila equipada no slot **Mochila** vira um inventário próprio, mostrado embaixo dos bolsos. O peso dela vem
do item (no Creative, o campo `Backpack`); os slots, do item ou de `Config.BackpackSlots`.

* Item recebido com os bolsos cheios vai para a mochila antes de cair no chão.
* Para tirar ou trocar, a mochila precisa estar vazia. Mochilas e maletas não entram uma na outra.
* **Nas costas:** no Creative, aparece no personagem automaticamente (usa o `Skinshop` do item e o `skinshop` da
  base, como o inventário antigo). Nas outras bases, defina a peça em `Config.EquipmentVisuals`:

```lua
Config.EquipmentVisuals = {
    backpack = { component = 5, male = { 45, 0 }, female = { 45, 0 } },   -- item = { drawable, textura }
}
```

### Acessórios como itens

```lua
Config.Accessories = { Enabled = true, Slots = { hat = { field = 'props', name = 'hat', index = 0 }, ... } }
```

Chapéu, óculos, brinco, máscara, corrente, relógio e pulseira ocupam os slots de equipamento ao lado do
personagem. Arrastar a peça para fora tira do personagem e vira um item (com o modelo e a cor), que pode ser
guardado, dado ou roubado; arrastar de volta veste. A loja de roupas continua funcionando: o que você compra lá
aparece no slot ao abrir o inventário, e cada mudança feita pelo inventário é gravada na sua loja de roupas.
Peças de um corpo (masculino/feminino) não vestem o outro.

### Rastro de evidência

```lua
Config.Evidence = { Enabled = true, Groups = { 'police' } }
```

Itens manuseados sem luvas (slot de equipamento `gloves` vazio) guardam a digital de quem mexeu (até 3). As
digitais não aparecem para os jogadores; quem está nos grupos acima tem **Analisar digitais** no menu do item e
pode colher a digital de alguém próximo para comparar. Itens com `flags.noPrints` não guardam digitais.

## items.lua

Sobrescreve ou cria itens. O que vem do framework (no Creative, `vrp/config/Item.lua`) é importado
automaticamente; aqui você só muda o que quiser:

```lua
Items['water'] = {
    consume = { thirst = 30, anim = 'drink', time = 3000, useLabel = 'Beber' }
}

Items['radio'] = { rarity = 'rare', category = 'tech' }
```

Campos: `label`, `description`, `weight` (kg), `stack`, `rarity` (`common`…`legendary`), `category`,
`image`, `maxCarry`, `durability` (horas), `unique`, `serial`, `consume`, `equip`, `container`, `weapon`, `flags`.

## Regras do servidor (arquivos abertos)

`server/open.lua` e `client/open.lua` não são alterados nas atualizações:

* `Hooks.GetPlayerWeight(src, charId)`: peso máximo (VIP, premium).
* `Hooks.CanSearch(src, target)`: quem pode ser revistado.
* `Hooks.GetCraftLevel(src, benchId)`: nível de fabricação (receitas com `level` acima ficam bloqueadas).
* `Hooks.HasBlueprint(src, item)`: se o jogador aprendeu a planta (receitas com `blueprint = true`).
* `Hooks.CanReadPrints(src)`: quem pode analisar digitais.
* `Hooks.GetTrunk(src, vehicle, plate)`: porta-malas personalizado (ex.: capacidade gravada por veículo).
* `ClientHooks.CanOpen()`: quando o jogador pode abrir.
* `ClientHooks.ApplyVitals(health, armor)`: como consumíveis curam.
