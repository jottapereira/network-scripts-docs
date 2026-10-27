---
description: Instalar a one_workshop em qualquer base, em poucos minutos.
---

# Instalação

## 1. Requisitos

* `one_lib` **v0.7.0 ou superior** (vem junto) e `oxmysql`.
* Um inventário: one\_inventory, ox\_inventory, qb-inventory ou o da sua base (ESX, Creative, vRPex).

## 2. Arquivos

Coloque `one_workshop` na pasta de recursos e garanta a ordem no `server.cfg`:

```cfg
ensure oxmysql
ensure one_lib
# seu framework e inventário
ensure one_workshop
```

As tabelas do banco são criadas sozinhas na primeira vez.

## 3. Itens

A oficina usa 24 itens: acessórios, munições especiais, tinta, kits de pintura e o cupom de skin. Eles só são
necessários nas categorias que cobram em itens (veja [Cobrança](cobranca.md)). Os arquivos de cadastro ficam em
`one_workshop/install/`. As imagens estão em `one_workshop/images/`.

{% tabs %}
{% tab title="one_inventory" %}
Nada a fazer: a oficina registra os itens e as imagens sozinha.
{% endtab %}

{% tab title="ox_inventory (ESX, Qbox)" %}
1. Cole o conteúdo de `install/ox_items.lua` dentro da tabela de `ox_inventory/data/items.lua`.
2. Copie `one_workshop/images/*.png` para `ox_inventory/web/images/`.

Os itens de acessório já vêm com a lista de componentes, então o ox também consegue montá-los pelo próprio
inventário.
{% endtab %}

{% tab title="qb-inventory (QBCore)" %}
1. Cole o conteúdo de `install/qb_items.lua` dentro de `QBShared.Items` em `qb-core/shared/items.lua`.
2. Copie `one_workshop/images/*.png` para `qb-inventory/html/images/`.
{% endtab %}

{% tab title="ESX (inventário padrão)" %}
Rode `install/esx_items.sql` no banco.
{% endtab %}

{% tab title="vRP Creative / vRPex" %}
1. Cole o conteúdo de `install/creative_items.lua` dentro de `List` em `vrp/config/Item.lua` (ou no arquivo de itens
   do seu inventário).
2. Copie as imagens para a pasta de imagens do inventário da base.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Mudou nomes de itens no config? Rode `workshop_export` no console do servidor para gerar os arquivos de cadastro de
novo.
{% endhint %}

## 4. Bancadas

Em `config.lua`, `Config.Benches`:

```lua
Config.Benches = {
	{ id = 'ammunation', type = 'armorer', coords = vec4(21.6, -1106.6, 28.8, 160.0), prop = 'prop_tool_bench02' },
	{ id = 'galpao', type = 'clandestine', coords = vec4(1272.4, -1712.1, 54.7, 25.0), prop = 'prop_tool_bench02' },
	{ id = 'praca', type = 'public', coords = vec4(-662.1, -935.3, 20.8, 180.0), prop = 'prop_tool_bench02', blip = { sprite = 110 } },
}
```

Os tipos (`public`, `armorer` e `clandestine`) e quem pode usar cada um ficam em `Config.BenchTypes`. Cada bancada
pode ter blip, atendente, comissão e preço próprio. Veja [Configuração](configuracao.md).

## 5. Skins

Ligue um ou mais pacotes de skins antes da oficina (`ensure one_skins_v1`). A oficina acha os pacotes sozinha. Passo a passo em
[Skins](skins.md) e [Pacotes de skins](pacotes.md).

## 6. Logs no Discord (opcional)

No `server.cfg`, nunca no config (o config vai para os jogadores):

```cfg
set one_workshop:webhook "https://discord.com/api/webhooks/..."
```

## 7. Antes de abrir para os jogadores

* `/oficina` e `/skinlab` (bancada de teste e vitrine das skins) só existem com `setr one_workshop:debug true` no `server.cfg`. Em produção deixe sem essa linha.
* Rode `workshop_selftest` no console: ele confere configuração, banco, pacotes, cobrança e as regras de compra e de aplicar. Todas as linhas precisam sair `ok`.
* Dê o ACE de admin para a staff: `add_ace group.admin oneworkshop.admin allow`.
