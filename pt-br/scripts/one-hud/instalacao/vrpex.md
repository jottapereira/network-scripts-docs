---
description: vRPex e vRP 1. Cerca de 5 minutos.
---

# Instalação: vRPex / vRP 1

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure vrp

ensure one_lib
ensure one_hud
```
{% endstep %}

{% step %}
### Desligue a HUD e as notificações da base

Tire do `server.cfg` a HUD que a sua base usa (`vrp_hud`, `nation_hud`...) e o `vrp_notify`, se houver. O evento
`Notify` dos scripts (`sucesso`, `negado`, `aviso`, `importante`) passa a aparecer no one\_hud.
{% endstep %}

{% step %}
### Telas do próprio vRP

No vRP 1, notificação, pedido (`vRP.request`) e campo de texto (`vRP.prompt`) ficam dentro do core. Adicione no
fim de `client_scripts` do `fxmanifest.lua` (ou `__resource.lua`) do `vrp`:

```lua
'@one_hud/bridge/vrp.lua'
```
{% endstep %}
{% endstepper %}

## Observações

* Fome e sede vêm do `vRP.getHunger/getThirst` (lidas a cada 15 s pelo servidor).
* Sem cinto na base, o one\_hud liga o próprio (`B`).
