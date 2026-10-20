---
description: Progresso, formulário, confirmação, pedido Y/N e texto de ajuda com a mesma API em qualquer base.
---

# Progress, Input, Confirm, Request, TextUI

Telas que todo script precisa. Com o [one\_hud](../../scripts/one-hud/README.md) instalado, aparecem no visual dele; sem
ele, caem no `ox_lib` (se houver) ou numa versão simples. O seu script não muda.

| Função | one\_hud | sem one\_hud |
|---|---|---|
| `One.Progress` | barra com animação, objeto na mão e cancelar | `ox_lib` progressBar · espera simples |
| `One.Input` | formulário com validação | `ox_lib` inputDialog |
| `One.Confirm` | confirmação (com "segurar para confirmar") | `ox_lib` alertDialog |
| `One.Request` | pedido Y/N sem tirar o controle | confirmação na tela |
| `One.TextUI` | texto de ajuda com a tecla | `ox_lib` textUI · ajuda nativa do GTA |
| [`One.Notify`](notify.md) | notificação do one\_hud | `ox_lib` · framework · nativa |

## Progress (cliente)

```lua
local ok = One.Progress({
    label = 'Arrombando fechadura', duration = 5000, icon = 'tool',
    canCancel = true,                                         -- tecla X (o jogador pode trocar)
    anim = { dict = 'mini@repair', clip = 'fixing_a_ped' },   -- ou { scenario = 'PROP_HUMAN_BUM_BIN' }
    prop = { model = 'prop_tool_screwdvr01', bone = 57005, pos = vec3(0.1, 0.0, 0.0), rot = vec3(0, 0, 0) },
    disable = { move = true, car = true, combat = true }
})
if not ok then return end   -- cancelou, morreu ou outro script cancelou
```

`One.Progress.Cancel()` e `One.Progress.IsActive()`.

## Input (cliente)

```lua
local values = One.Input({
    eyebrow = 'Comando · /multar', title = 'Emitir multa', icon = 'file', submit = 'Emitir',
    fields = {
        { type = 'number', name = 'target', label = 'ID do cidadão', required = true, min = 1, half = true },
        { type = 'money', name = 'amount', label = 'Valor', required = true, min = 50, max = 25000, half = true },
        { type = 'select', name = 'reason', label = 'Infração', required = true,
          options = { { value = 'speed', label = 'Excesso de velocidade' } } },
        { type = 'textarea', name = 'notes', label = 'Observações', maxLength = 200 },
        { type = 'checkbox', name = 'points', label = 'Adicionar pontos na CNH', default = true }
    }
})
if not values then return end           -- cancelou
print(values.amount, values[2])         -- por nome e por posição
```

Tipos: `text`, `number`, `password`, `textarea`, `select`, `radio`, `checkbox`, `slider`, `money`, `date`.
Validação: `required`, `min`, `max`, `minLength`, `maxLength`, `pattern` (+ `patternError`).

## Confirm (cliente)

```lua
local sell = One.Confirm({
    eyebrow = 'Concessionária', title = 'Vender este veículo?', text = 'Essa ação não pode ser desfeita.',
    danger = true, hold = 1200, confirm = 'Vender',
    details = { { 'Veículo', 'Sultan RS' }, { 'Você recebe', '$ 18.500' } }
})
```

## Request (servidor ou cliente)

```lua
-- servidor: espera o jogador apertar Y/N (ou o tempo acabar)
local accepted = One.Request(target, {
    eyebrow = 'Transferência', title = ('%s quer te dar $ 500'):format(name), icon = 'cash', time = 15000
})
```

Pedidos de vários scripts entram numa fila; o jogador continua andando e dirigindo enquanto responde.

## TextUI (cliente)

```lua
One.TextUI('Abrir o porta-malas', { key = 'E' })
One.TextUI(false)
```
