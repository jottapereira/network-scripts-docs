---
description: QBCore com qb-inventory (ou forks: ps-inventory, lj-inventory). Cerca de 10 minutos.
---

# Instalação: QBCore

O QBCore entrega os itens chamando `exports['qb-inventory']` (`Player.Functions.AddItem`, `RemoveItem`...). O
one\_inventory **responde por esses exports** e mantém o `PlayerData.items` sempre em dia, então o qb-core, o
qb-shops e os demais scripts continuam funcionando.

{% hint style="warning" %}
Requer um **qb-core de 2023 ou mais novo** (o que chama `exports['qb-inventory']` para mexer em itens). Versões
antigas guardavam o inventário dentro do próprio qb-core e não passam pelo one\_inventory.
{% endhint %}

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure qb-core

ensure one_lib
ensure one_inventory
```

Depois deles vêm os demais recursos da base (as pastas `qb` e `standalone`).
{% endstep %}

{% step %}
### Desligue o qb-inventory

Tire `qb-inventory` (ou `ps-inventory`, `lj-inventory`) do `server.cfg`. Se a sua base usa `ensure [qb]`, mova a
pasta para fora de `[qb]`. O one\_inventory se declara `qb-inventory` (`provide`): dependências continuam
satisfeitas.
{% endstep %}

{% step %}
### Migre os inventários

No console do servidor:

```
oneinv_migrate qb
```

Copia jogadores (`players.inventory`), baús (`stashitems`/`inventories`), porta-malas e porta-luvas. A origem não
é apagada. Depois, reinicie o one\_inventory.
{% endstep %}

{% step %}
### Imagens

Copie `qb-inventory/html/images/` para `one_inventory/web/images/`. `refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_inventory] 420 itens registrados (qb)
[one_inventory] compatibilidade qb-inventory ativa
```

## Observações

* **Itens:** `QBCore.Shared.Items` (peso em gramas, convertido) e o tipo de munição de `QBCore.Shared.Weapons`.
* **Itens usáveis** (`QBCore.Functions.CreateUseableItem`) continuam funcionando.
* **Dinheiro:** `cash` e `bank`. O QBCore não tem conta de dinheiro sujo: para lojas ilegais use
  `currency = 'markedbills'` (ou o item que a sua base usa).
* **qb-target:** a mira continua sendo dele; o porta-malas aparece dentro do qb-target.
* **Roupa** (acessórios como itens): `illenium-appearance`. `qb-clothing` ainda não é suportado.
