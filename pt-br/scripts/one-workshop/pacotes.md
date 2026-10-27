---
description: Como a oficina usa pacotes de skins, como ligar vários e como criar o seu.
---

# Pacotes de skins

As skins não vêm dentro da oficina: elas vêm em **pacotes** (recursos separados). Você pode ligar quantos quiser: o
pacote da Network One, os de outros criadores ou os seus. A oficina junta todos numa galeria só, com filtro por coleção.

## Ligar pacotes

Ligue cada pacote **antes** da oficina:

```cfg
ensure one_skins_v1
ensure pacote_do_fulano
ensure one_workshop
```

No `config.lua`, em `Config.Skins`:

```lua
Config.Skins.packs = 'auto'                        -- todo pacote iniciado que se declara (padrão)
Config.Skins.packs = { 'one_skins_v1', 'outro' }   -- ou só estes, nesta ordem
```

Ajustes por pacote:

```lua
Config.Skins.packOptions = {
	one_skins_v1 = { factor = 1.0 },                       -- multiplica os preços do pacote
	pacote_vip = { access = { groups = { 'vip' } } },      -- só VIP compra e usa
	pacote_antigo = { enabled = false },                   -- desliga sem desinstalar
}
```

O console mostra o que foi encontrado: `workshop_skins`.

## Formato de um pacote

Um pacote é um recurso FiveM com:

1. as skins no formato do jogo (modelos e texturas em `stream/`, `weaponcomponents.meta` e `weaponarchetypes.meta`);
2. um `skins.json` com o índice;
3. no `fxmanifest.lua`, a linha que o declara:

```lua
one_workshop_pack 'skins.json'
```

`skins.json`:

```json
{
  "format": 1,
  "name": "Nome da coleção",
  "author": "Seu nome",
  "version": "1.0.0",
  "skins": [
    {
      "weapon": "WEAPON_ASSAULTRIFLE",
      "component": "COMPONENT_ASSAULTRIFLE_SKIN_V1_DRAGAO",
      "style": "dragao",
      "label": "Dragão",
      "model": "w_ar_assaultrifle_v1dragao",
      "collection": "Lateral",
      "tier": "legendary",
      "price": { "cash": 250000, "gems": 900 }
    }
  ]
}
```

| Campo | Obrigatório | O que é |
|---|---|---|
| `weapon` | sim | arma (`WEAPON_...`) |
| `component` | sim | nome do componente da skin (único em todos os pacotes) |
| `style` | sim | identificador do estilo (usado nas regras do `config.lua`) |
| `label` | não | nome mostrado (padrão: `style`) |
| `collection` | não | agrupamento na galeria (padrão: o nome do pacote) |
| `tier` | não | `common`, `rare`, `epic` ou `legendary` |
| `price` | não | preço próprio (`cash`, `gems`, `items`), no lugar do preço da raridade |

O dono do servidor sempre pode sobrescrever no `config.lua`: raridade (`Config.Skins.tier`), preço
(`Config.Skins.override`), acesso (`Config.Skins.access`) e skins iniciais (`Config.Skins.starter`).

## Limite do jogo

A definição de cada arma aceita **12 componentes** no encaixe das skins, contando os acabamentos que o próprio jogo já
põe lá. Por isso um pacote traz até ~10 skins por arma. Pacotes que passam disso são cortados pelo mesclador, que avisa
no console.

## Gerar o pacote no seu PC

O pacote da Network One é gerado com a ferramenta `tools/skins` a partir do **seu** GTA V (ver `tools/skins/README.md`).
Os arquivos gerados contêm dados do jogo e **não** devem ser publicados nem revendidos.
