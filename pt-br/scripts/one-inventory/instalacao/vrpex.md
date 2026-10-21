---
description: "vRPex e vRP 1: com o inventário dentro do vrp ou num recurso separado (ex.: lotus). Cerca de 5 minutos."
---

# Instalação: vRPex / vRP 1

Existem dois tipos de base vRPex. Você não precisa descobrir qual é a sua: o passo a passo é o mesmo, e o
one\_inventory avisa no console se faltar alguma coisa.

| Tipo | Como reconhecer | O que o one\_inventory faz |
|---|---|---|
| Inventário **dentro do vrp** (vRP 1 clássico) | não existe uma pasta `inventory` separada | assume as funções de item do vrp |
| Inventário **em recurso separado** (lotus e derivados) | existe a pasta `inventory` com `config/shared.items.lua` | assume as funções de item do vrp **e** importa o uso dos itens da sua base (comer, beber, remédio, drogas, lockpick...) |

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure vrp

ensure one_lib
ensure one_inventory

# depois: os scripts da base
```
{% endstep %}

{% step %}
### Ligue a ponte no vRP

No `fxmanifest.lua` (ou `__resource.lua`) do recurso `vrp`, adicione **uma linha no fim** de `server_scripts`:

```lua
server_scripts {
    -- ... o que já estava aqui ...
    '@one_inventory/bridge/vrp.lua'
}
```
{% endstep %}

{% step %}
### Só se a sua base tem a pasta `inventory`: importe o uso dos itens

Com o servidor ligado (o `inventory` antigo ainda pode estar ligado), digite no **console do servidor**:

```
oneinv_import
```

Depois:

1. Tire `ensure inventory` do `server.cfg` (o one\_inventory substitui).
2. **Não apague a pasta `inventory`**: o `vrp` ainda lê a lista de itens de lá.
{% endstep %}

{% step %}
### Imagens

Copie os PNG dos itens para `one_inventory/web/images/<item>.png`. Na base com a pasta `inventory`, as imagens
geralmente estão em `inventory/web/build/...` (procure por arquivos `.png` com o nome dos itens). Item sem imagem
mostra o ícone da categoria.
{% endstep %}

{% step %}
### Reinicie

`refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_inventory] vRPex: itens lidos de inventory/config/shared.items.lua
[one_inventory] ponte vRP ativa
[one_inventory] uso de itens da base (lotus): 84 itens ligados      ← só na base com a pasta inventory
```

Se aparecer `uso de itens da base não importado: rode "oneinv_import"`, faltou o passo 3.

## O que vem da sua base, sem você mexer em nada

* **Itens:** nome, peso, imagem e tipo, de onde a base guardar (`inventory/config/shared.items.lua`,
  `vrp/cfg/items.lua`...). Armas ganham a munição certa automaticamente (`weapon_x` → `ammo_x`).
* **Uso dos itens:** a mesma função de antes, com as mesmas animações, barras e efeitos.
* **Peso que o jogador carrega:** a regra da sua base (mochila, VIP, grupos), a mesma de antes.
* **Itens que os jogadores já tinham:** entram nos bolsos na primeira vez que cada um entra (o que não couber cai
  no chão ao lado; nada se perde).
* **Aviso de item recebido/removido:** o mesmo da sua base.

## Observações

* **Baús da base** (`inventory/data/chests.json`) não são migrados: use os baús do one\_inventory.
* **Armas do vRP 1** no formato `wbody|WEAPON_PISTOL` / `wammo|WEAPON_PISTOL` viram a arma e a munição do
  one\_inventory na migração.
* **Dinheiro sujo** é um item (padrão `dinheirosujo`, convar `one:vrpex:dirty_item`).
* **Grupos sem cargo:** lojas, bancadas e baús com `groups = { policia = 0 }` funcionam; grade acima de 0 nunca
  passa no vRP 1.
