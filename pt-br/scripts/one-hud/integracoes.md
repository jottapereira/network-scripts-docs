---
description: Exports de cliente e servidor para usar as telas e a HUD nos seus scripts.
---

# Integração com outros scripts

{% hint style="info" %}
Escrevendo um script novo? Prefira o [one\_lib](../../one-lib/modulos/tela.md) (`One.Notify`, `One.Progress`,
`One.Input`...): ele usa o one\_hud quando existe e cai no ox\_lib quando não.
{% endhint %}

## Cliente

```lua
local hud = exports.one_hud

hud:Notify({ type = 'success', title = 'Pago', description = 'Você recebeu $ 500', duration = 5000 })
-- type: info | success | error | warning | money | police

local ok = hud:Progress({ label = 'Arrombando', duration = 5000, canCancel = true,
    anim = { dict = 'mini@repair', clip = 'fixing_a_ped' }, disable = { move = true, combat = true } })
hud:CancelProgress() · hud:IsProgressActive()

local values = hud:Input({ title = 'Multar', fields = { { type = 'money', name = 'amount', label = 'Valor', min = 50 } } })
local yes = hud:Confirm({ title = 'Vender?', danger = true, hold = 1200, details = { { 'Placa', 'ABC123' } } })
local accepted = hud:Request({ title = 'Ana quer te dar $ 500', time = 15000 })

hud:TextUI('Abrir o porta-malas', { key = 'E' }) · hud:HideTextUI() · hud:IsTextUIOpen()
hud:Subtitle('Siga o atendente até o cofre', 8000)
hud:SetObjective({ title = 'Roubo à loja', remaining = 160, steps = { { label = 'Renda o atendente', done = true }, { label = 'Fuja' } } })
hud:ClearObjective()

hud:SetChip('wanted', { label = 'Procurado', icon = 'siren', seconds = 300, max = 300, tone = 'danger' })
hud:ClearChip('wanted')

hud:SetVisible(false)   -- cada recurso tem a sua trava; parar o recurso libera
hud:IsVisible()
```

Formulário: tipos `text`, `number`, `password`, `textarea`, `select`, `radio`, `checkbox`, `slider`, `money`,
`date`; validação `required`, `min`, `max`, `minLength`, `maxLength`, `pattern`. Retorno por `name` e por posição.

## Servidor

```lua
exports.one_hud:Notify(source, { type = 'info', description = 'Olá' })
local accepted = exports.one_hud:Request(source, { title = 'Aceita a proposta?', time = 20000 })
local values = exports.one_hud:Input(source, { title = 'Nome da empresa', fields = { { type = 'text', name = 'name', label = 'Nome' } } })
local ok = exports.one_hud:Confirm(source, { title = 'Confirmar compra?' })
local done = exports.one_hud:Progress(source, { label = 'Processando', duration = 3000 })
```

Tudo que chega do cliente deve ser validado no servidor antes de usar.

## Eventos que o one\_hud escuta

| Evento | Base | Efeito |
|---|---|---|
| `Notify` | vRP (todas) | notificação (cor/tipo da base) |
| `NotifyItem` | Creative | aviso de item |
| `Progress` | Creative | barra de progresso |
| `hud:Active` · `hud:client:ToggleHud` · `esx_hud:HudToggle` | todas | esconder/mostrar a HUD |
| `hud:Hunger/Thirst/Stress` · `hud:client:UpdateNeeds/UpdateStress` · `esx_status:onTick` | por base | status |
