---
description: Qbox (qbx_core + ox_inventory). Cerca de 10 minutos.
---

# Instalação: Qbox

O Qbox usa o `ox_inventory` como inventário. O one\_inventory **responde pelos exports dele** (servidor e cliente),
então o `qbx_core` e os scripts do Qbox funcionam sem alteração.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure ox_lib
ensure qbx_core

ensure one_lib
ensure one_inventory
```

Depois deles vêm os demais recursos da base (as pastas `qbx` e `standalone`).
{% endstep %}

{% step %}
### Desligue o ox\_inventory (mantenha a pasta)

Tire `ensure ox_inventory` do `server.cfg` e **deixe a pasta no servidor**: a lista de itens é lida de
`ox_inventory/data/items.lua` e `data/weapons.lua`. O one\_inventory se declara `ox_inventory` (`provide`), então
a dependência do `qbx_core` continua satisfeita.
{% endstep %}

{% step %}
### Migre os inventários

```
oneinv_migrate ox
```

Copia jogadores, baús, porta-malas e porta-luvas. A origem não é apagada. Depois, reinicie o one\_inventory.
{% endstep %}

{% step %}
### Imagens

Copie `ox_inventory/web/images/` para `one_inventory/web/images/`. `refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_inventory] 400 itens registrados (qbox)
[one_inventory] compatibilidade ox_inventory ativa
```

## Observações

* **Itens usáveis** (`exports.qbx_core:CreateUseableItem`) continuam funcionando.
* **Dinheiro:** `cash` e `bank`; sem conta de dinheiro sujo (use o item da sua base como `currency`).
* **ox\_target:** a mira continua sendo dele; o porta-malas aparece dentro do ox\_target.
* **Roupa** (acessórios como itens): `illenium-appearance`.
