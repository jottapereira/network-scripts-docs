---
description: Escreva um script que roda em qualquer framework usando o one_lib.
---

# Usando o one\_lib no seu script

O `one_lib` é aberto: você pode usá-lo nos seus próprios scripts e ganhar compatibilidade com Creative,
ESX, QBCore, Qbox e Standalone sem escrever uma linha específica de framework.

## 1. Manifest

```lua
fx_version 'cerulean'
game 'gta5'
lua54 'yes'

dependencies { 'one_lib' }

shared_scripts {
    '@one_lib/init.lua',
    'config.lua'
}

client_scripts { 'client/*.lua' }
server_scripts { 'server/*.lua' }

files { 'locales/*.lua' }
```

## 2. Um exemplo completo

Uma loja que vende água, com preço no servidor, rate limit e log:

```lua
-- server/main.lua
local PRICE = 6

One.Callback.Register('mystore:buyWater', function(src)
    if not One.Player.IsLoaded(src) then return false end

    local paidWith = One.Money.Pay(src, PRICE)
    if not paidWith then
        One.Notify(src, One.Locale('no_money'), 'error')
        return false
    end

    -- entregar o item com o inventário do seu servidor
    One.Log.Audit('mystore', src, 'Comprou água', { price = PRICE, account = paidWith })
    One.Notify(src, One.Locale('bought'), 'success')
    return true
end, { rate = { max = 2, window = 1000 } })
```

```lua
-- client/main.lua
RegisterCommand('agua', function()
    One.Callback.Await('mystore:buyWater')
end)
```

```lua
-- locales/pt-BR.lua
return {
    ['no_money'] = 'Dinheiro insuficiente',
    ['bought'] = 'Você comprou uma água'
}
```

Esse script roda igual em todas as bases suportadas.

## 3. Regras de ouro

1. **Nunca chame o framework direto** (`vRP.*`, `ESX.*`, `QBCore.*`). Se o `one_lib` não cobre algo, peça no Discord.
2. **O servidor decide.** O cliente pede; preço, quantidade e permissão são calculados no servidor.
3. **Valide tudo que vem do cliente** com [`One.Utils`](../one-lib/modulos/utils.md).
4. **Sem loop sem necessidade.** Use [`One.Cache`](../one-lib/modulos/cache.md) em vez de um loop para saber se o jogador está num veículo.
