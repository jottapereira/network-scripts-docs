---
description: Servidor sem framework (ou com framework próprio). Cerca de 5 minutos.
---

# Instalação: Standalone

Sem framework, o [one\_lib](../../../one-lib/README.md) cuida do personagem (com o `one_characters`, ou um por
conta) e o one\_inventory é o único dono dos itens.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql

ensure one_lib
ensure one_inventory
```

Se o one\_lib não detectar sozinho, force: `setr one:framework "standalone"`.
{% endstep %}

{% step %}
### Cadastre os itens

Em `one_inventory/items.lua`:

```lua
Items = {
    water = { label = 'Água', weight = 0.5, stack = 10, category = 'drink',
              consume = { thirst = 35, anim = 'drink', time = 2500 } },
    burger = { label = 'Hambúrguer', weight = 0.25, stack = 10, category = 'food',
               consume = { hunger = 30, anim = 'eat', time = 3000 } },
}
```

Se a pasta `ox_inventory` estiver no servidor (mesmo parada), a lista dela (`data/items.lua`) é importada
automaticamente.

Outros scripts podem registrar itens e usos:

```lua
exports.one_inventory:RegisterItem('lockpick', { label = 'Lockpick', weight = 0.1, stack = 10 })
exports.one_inventory:RegisterUsable('water', function(source, item, slot)
    -- efeito; return false para não consumir
end)
```
{% endstep %}

{% step %}
### Imagens

`one_inventory/web/images/<item>.png`. Item sem imagem mostra o ícone da categoria.
{% endstep %}
{% endstepper %}

## Observações

* **Dinheiro e grupos** não existem sem framework: lojas cobram com item (`currency = 'cash'` só funciona se o
  seu servidor tiver um adapter de dinheiro). Grupos usam ACE (`add_ace group.police one.group.police allow`).
