---
description: Dados do jogador local mantidos por um único loop compartilhado.
---

# Cache

Um único loop de 100 ms no `one_lib` mantém estes valores para **todos** os scripts. Ler é acessar uma
tabela, sem chamar natives.

| Campo | Valor |
|---|---|
| `One.Cache.ped` | ped do jogador |
| `One.Cache.playerId` | id local do jogador |
| `One.Cache.serverId` | id do jogador no servidor |
| `One.Cache.vehicle` | veículo atual ou `false` |
| `One.Cache.seat` | assento (`-1` = motorista) ou `false` |
| `One.Cache.weapon` | arma na mão ou `false` |

## Reagir a mudanças

```lua
One.Cache.OnChange('vehicle', function(vehicle, previous)
    if vehicle then
        -- entrou num veículo: mostrar velocímetro
    end
end)
```

{% hint style="info" %}
Ausência é sempre `false`, nunca `nil`.
{% endhint %}
