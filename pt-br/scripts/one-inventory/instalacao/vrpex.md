---
description: vRPex e vRP 1 (user_id, inventário no core do vRP). Cerca de 5 minutos.
---

# Instalação: vRPex / vRP 1

No vRP 1 o inventário fica **dentro do core** (`vrp/modules/inventory.lua`), sem recurso separado. O one\_inventory
assume as funções de item do core por uma ponte, e o resto da base continua igual.

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
### Imagens

Copie os PNG dos itens para `one_inventory/web/images/<item>.png` (o vRP 1 não tem imagens próprias; a maioria
das bases usa as do inventário em NUI que tiver instalado). Item sem imagem mostra o ícone da categoria.
{% endstep %}

{% step %}
### Reinicie

`refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como os itens chegam

* **Itens fixos:** `vrp/cfg/items.lua` e os pacotes de `cfg/item/*.lua` que ele carrega (nome, descrição, peso).
* **Itens de scripts:** quem chama `vRP.defInventoryItem(...)` registra o item no one\_inventory na hora.
* **Uso:** o item usa a **escolha principal** do menu antigo do vRP ("Usar", "Comer", "Beber", "Equipar"...),
  com a mesma função de antes. Dar e jogar fora são do one\_inventory.

## Como saber que deu certo

```
[one_inventory] 140 itens registrados (vrpex)
[one_inventory] ponte vRP ativa
```

## Observações

* **Armas do vRP 1** no formato `wbody|WEAPON_PISTOL` / `wammo|WEAPON_PISTOL` continuam funcionando pelo menu
  antigo do vRP. Para armas como item no one\_inventory (na mão, munição, acessórios), declare em `items.lua`
  itens `WEAPON_*` e as munições correspondentes.
* **Dinheiro sujo** é um item (padrão `dinheirosujo`, convar `one:vrpex:dirty_item`).
* **Grupos sem cargo:** lojas, bancadas e baús com `groups = { policia = 0 }` funcionam; grade acima de 0 nunca
  passa no vRP 1.
