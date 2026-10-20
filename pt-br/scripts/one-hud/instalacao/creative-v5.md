---
description: vRP Creative v4/v5 (vrp_creative, vrp_hud, vrp_notify). Cerca de 5 minutos.
---

# Instalação: vRP Creative v4/v5

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure vrp

ensure one_lib
ensure one_hud

ensure [vrp]
```
{% endstep %}

{% step %}
### Desligue a HUD e as notificações da base

Tire `vrp_hud` e `vrp_notify` do `server.cfg` (mantenha as pastas). O evento `Notify` que os scripts disparam
passa a aparecer no one\_hud, com o tipo certo (`sucesso`, `negado`, `aviso`, `importante`).
{% endstep %}

{% step %}
### Opcional: telas do próprio vRP

Para que `vRP.request` (sim/não) e `vRP.prompt` (campo de texto) do core também usem o one\_hud, adicione no fim de
`client_scripts` do `fxmanifest.lua` do `vrp`:

```lua
'@one_hud/bridge/vrp.lua'
```
{% endstep %}
{% endstepper %}

## Observações

* Fome e sede vêm do vRP (o one\_hud lê a cada 15 s pelo servidor).
* Sem cinto na base, o one\_hud liga o próprio (`B`).
