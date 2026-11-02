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

## O pacote que vem com a compra

A compra da oficina inclui o pacote **one_skins_v1**: 240 skins para 39 armas, desenhadas e modeladas do zero pela Network One, com
miniaturas para a bancada. O `one_skins_v1.zip` traz o recurso pronto, o mesclador das metas e um `LEIA-ME.txt` com a instalação:
copiar a pasta, rodar o mesclador (`node merge-metas.js ... --apply`), ligar `ensure one_skins_v1` antes da oficina e reconectar.

## Gerar o pacote no seu PC

O pacote da Network One é gerado com a ferramenta `tools/skins` a partir do **seu** GTA V (ver `tools/skins/README.md`).
Os arquivos gerados contêm dados do jogo e **não** devem ser publicados nem revendidos.

### Passo a passo

1. Instale o **.NET 8 Runtime** (só o runtime; não precisa do SDK) e tenha o GTA V instalado no mesmo computador.
2. Baixe e extraia o `skinpack.zip` que vem com a compra. Ele traz o gerador, o `assign-original.json` (as skins de cada arma) e um `LEIA-ME.txt`.
3. Crie um `armas.txt` com uma arma por linha (`WEAPON_PISTOL`, `WEAPON_CARBINERIFLE`...) e rode:

   ```
   SkinPack.exe pack "C:\...\Grand Theft Auto V" "C:\servidor\resources\one_skins_v1" --weapons armas.txt --styles fenix --assign assign-original.json --tag v1 --name one_skins_v1 --cap 1024
   ```

   Leva de 2 a 3 minutos para umas 40 armas. Para ver uma skin sem abrir o jogo: `SkinPack.exe look "C:\...\Grand Theft Auto V" WEAPON_PISTOL previa fenix`.
4. Rode o mesclador nas metas do servidor (seção acima) e ligue o recurso no `server.cfg` (`ensure one_skins_v1`).
5. Reinicie o servidor e **reconecte** (o jogo só baixa os arquivos novos ao conectar).

O pacote gerado leva as miniaturas da oficina em `thumbs/` quando você as gera com `SkinPack thumbs` (opcional: sem elas, o cartão mostra um desenho).
