---
description: Escolha a sua base e siga o passo a passo. Cada guia leva de 5 a 10 minutos.
---

# Instalação

O one\_inventory funciona em qualquer base suportada pelo [one\_lib](../../one-lib/README.md). O que muda de uma
base para outra é **o que desligar** e **de onde vêm os itens e as imagens**. Escolha a sua:

| Base | Guia | Itens vêm de | O que você desliga |
|---|---|---|---|
| vRP Creative (Network, Origens, Bewitched...) | [Creative](instalacao/creative.md) | `vrp/config/Item.lua` | `inventory`, `chest`, `shops`, `trunkchest`, `inspect`, `crafting` |
| vRP Creative v4/v5 | [Creative v4/v5](instalacao/creative-v5.md) | `vrp/modules/inventory.lua` | `vrp_inventory` |
| vRPex / vRP 1 | [vRPex](instalacao/vrpex.md) | `vrp/cfg/items.lua` + scripts | nada |
| ESX Legacy | [ESX](instalacao/esx.md) | `ox_inventory/data/items.lua` ou tabela `items` | `ox_inventory` (ou o inventário que usar) |
| QBCore | [QBCore](instalacao/qbcore.md) | `qb-core/shared/items.lua` | `qb-inventory` |
| Qbox | [Qbox](instalacao/qbox.md) | `ox_inventory/data/items.lua` | `ox_inventory` |
| Standalone | [Standalone](instalacao/standalone.md) | `items.lua` do one\_inventory | nada |

## Comum a todas as bases

* **Requisitos:** `oxmysql` e [`one_lib`](../../one-lib/instalacao.md) **0.5 ou mais novo**, iniciado antes do inventário.
* **Banco:** as tabelas (`one_inventory`, `one_inventory_shops`, `one_inventory_crafting`) são criadas sozinhas.
* **Ordem no `server.cfg`:**

```cfg
ensure oxmysql
ensure <seu framework>

ensure one_lib
ensure one_inventory

# depois: os demais scripts da base
```

{% hint style="warning" %}
**Tirar o inventário antigo do `server.cfg` não é apagar a pasta.** Em várias bases o one\_inventory **lê**
arquivos dele (lista de itens, imagens, gameplay importado). Deixe a pasta no servidor; só não dê `ensure`.
Se a sua base usa `start [pasta]`, mova o recurso antigo para uma pasta que não inicia (ex.: `[disabled]`).
{% endhint %}

## Depois de instalar

1. Entre no servidor e aperte **TAB**: o inventário abre com os seus itens.
2. No console do servidor, `oneinv_images` lista os itens que ficaram sem imagem.
3. Ajuste o que quiser em [Configuração](configuracao.md).
4. Algo estranho? Veja [Problemas comuns](problemas-comuns.md).

## Teclas padrão

| Tecla | Ação |
|---|---|
| `TAB` | abrir/fechar (chão perto de você; porta-luvas dentro do veículo) |
| `1` a `5` | usar o item fixado no slot rápido |
| `E` (perto de loja, bancada, baú) | abrir pela marca de interação |
| `ALT` mirando no veículo | porta-malas e demais opções |

O jogador pode trocar todas em **Configurações > Atalhos > FiveM**.
