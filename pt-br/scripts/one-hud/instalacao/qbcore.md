---
description: QBCore (qb-hud, progressbar, qb-input, notificações do qb-core). Cerca de 10 minutos.
---

# Instalação: QBCore

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure qb-core

ensure one_lib
ensure one_hud

# depois: [qb], [standalone]...
```
{% endstep %}

{% step %}
### Desligue o que o one\_hud substitui (mantenha as pastas)

Tire do `server.cfg` (ou mova para fora de `[qb]`): `qb-hud`, `progressbar` e `qb-input`.
`exports['progressbar']:Progress` e `exports['qb-input']:ShowInput` passam a abrir as telas do one\_hud, com o mesmo
retorno.
{% endstep %}

{% step %}
### A linha no qb-core (obrigatória)

A notificação (`QBCore.Functions.Notify`, evento `QBCore:Notify`), a barra (`QBCore.Functions.Progressbar`, que no
original exige o `progressbar` ligado) e o `DrawText` ficam dentro do qb-core. No `qb-core/fxmanifest.lua`, no fim
de `client_scripts`:

```lua
'@one_hud/bridge/qb-core.lua'
```
{% endstep %}
{% endstepper %}

## Como saber que deu certo

`QBCore.Functions.Notify('teste', 'success')` (por qualquer script) aparece à direita, no visual do one\_hud.

## Observações

* **Fome, sede, estresse, dinheiro, emprego:** atualizam na hora (`QBCore:Player:SetPlayerData`).
* **Cinto:** o do `qb-smallresources` é usado (ícone no velocímetro); sem ele, o one\_hud liga o próprio.
* **Voz:** pma-voice (alcance, falando, rádio).
* **qb-menu** continua com a tela dele (menu de contexto fica para uma versão futura).
