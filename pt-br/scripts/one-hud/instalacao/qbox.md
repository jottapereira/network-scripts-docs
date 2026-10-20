---
description: Qbox (qbx_core + ox_lib). Cerca de 5 minutos.
---

# Instalação: Qbox

O Qbox usa o ox\_lib para todas as telas. Com **uma linha no ox\_lib**, `lib.notify`, `lib.progressBar`,
`lib.inputDialog`, `lib.alertDialog` e `lib.showTextUI` de **todos** os scripts aparecem no one\_hud, com o mesmo
retorno.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure ox_lib
ensure qbx_core

ensure one_lib
ensure one_hud
```

Depois deles vêm os demais recursos da base (as pastas `qbx` e `standalone`).
{% endstep %}

{% step %}
### Desligue a HUD da base

Tire `qbx_hud` (ou a HUD que usar) do `server.cfg`.
{% endstep %}

{% step %}
### A linha no ox\_lib

No `ox_lib/fxmanifest.lua`, no fim de `client_scripts`:

```lua
'@one_hud/bridge/ox_lib.lua'
```
{% endstep %}
{% endstepper %}

## Observações

* **Fome, sede, estresse:** statebags do Qbox (`hunger`, `thirst`, `stress`) e metadata.
* **Cinto:** o do `qbx_seatbelt` é usado; sem ele, o one\_hud liga o próprio.
* **Menu de contexto** (`lib.registerContext`) e **skill check** continuam com o ox\_lib.
