---
description: Notificações que aparecem no sistema de notificação do servidor.
---

# Notify

```lua
-- servidor
One.Notify(src, 'Compra realizada', 'success')
One.Notify(src, { title = 'Banco', description = 'Saldo insuficiente', type = 'error', duration = 6000 })

-- cliente
One.Notify('Você está sem combustível', 'warning')
```

Tipos: `success`, `error`, `warning`, `info`.

## Para onde vai

Na ordem, o primeiro disponível:

1. `one_notify` (quando lançado)
2. `ox_lib`
3. o sistema do framework (Creative `Notify`, ESX `esx:showNotification`, QBCore `QBCore:Notify`, Qbox `qbx_core:Notify`)
4. notificação nativa do GTA

Force com `setr one:notify "ox"` (`one`, `ox`, `framework` ou `native`).
