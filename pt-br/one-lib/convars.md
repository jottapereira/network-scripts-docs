---
description: Configurações globais do one_lib pelo server.cfg. Todas são opcionais.
---

# Convars

{% hint style="warning" %}
Use `setr` para o que o cliente também precisa ler e `set` para o que deve ficar só no servidor.
**Webhooks sempre com `set`**, para que nunca cheguem ao jogador.
{% endhint %}

## Gerais

| Convar | Tipo | Padrão | Descrição |
|---|---|---|---|
| `one:framework` | `setr` | `auto` | força o framework: `creative`, `creativev5`, `vrpex`, `esx`, `qb`, `qbox`, `standalone` |
| `one:appearance` | `setr` | `auto` | força o sistema de roupa: `creative`, `illenium`, `skinchanger`, `one` |
| `one:locale` | `setr` | `pt-BR` | idioma padrão de todos os produtos |
| `one:notify` | `setr` | `auto` | notificações: `one`, `ox`, `framework`, `native` |
| `one:accent` | `setr` | verde Network One | cor de destaque das telas de todos os produtos (`"#ff6a00"` ou `"255, 106, 0"`). Ver [Cor das telas](../comece-aqui/cor-das-telas.md) |
| `one:sounds` | `setr` | `true` | `false` desliga os sons de interface de todos os produtos |
| `one:interact_aim` | `setr` | `auto` | mira (ALT) da interação: `auto` (usa ox\_target/qb-target se a base tiver), `one` (sempre a do one\_lib), `external` (sempre delegar) |
| `one:log_level` | `set` | `info` | `debug`, `info`, `warn` ou `error` |

## Webhooks

| Convar | Descrição |
|---|---|
| `one:webhook:exploit` | alertas de ação suspeita (cliente tentando o que não devia) |
| `one:webhook:audit` | auditoria geral |
| `one:webhook:characters` | criação e exclusão de personagens |
| `one:webhook:<canal>` | qualquer canal usado por um produto |

```cfg
set one:webhook:exploit "https://discord.com/api/webhooks/..."
set one:webhook:characters "https://discord.com/api/webhooks/..."
```

Os envios respeitam o limite do Discord (uma mensagem por segundo, em fila).

## Por framework

| Convar | Padrão | Descrição |
|---|---|---|
| `one:creative:cash_item` | `dollar` | item usado como dinheiro em espécie |
| `one:creative:dirty_item` | `dirtydollar` | item usado como dinheiro sujo |
| `one:creative:premium_slots` | `2` | slots extras de personagem para contas Premium |
| `one:creativev5:cash_item` | `dollars` | Creative v4/v5: item usado como dinheiro em espécie |
| `one:creativev5:dirty_item` | `dollars2` | Creative v4/v5: item usado como dinheiro sujo |
| `one:esx:prefix` | `char` | prefixo dos personagens (`char1:...`) |
| `one:esx:height` | `180` | altura gravada em personagens novos |
| `one:vrpex:dirty_item` | `dinheirosujo` | item usado como dinheiro sujo |

## Exemplo completo

```cfg
setr one:locale "pt-BR"
setr one:notify "auto"
set one:log_level "info"
set one:webhook:exploit "https://discord.com/api/webhooks/..."
```
