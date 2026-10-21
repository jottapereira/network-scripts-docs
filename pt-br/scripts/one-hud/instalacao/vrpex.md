---
description: "vRPex e vRP 1, com ou sem HUD própria da base (ex.: lotus). Cerca de 5 minutos."
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
### Telas do próprio vRP

No vRP 1, notificação, pedido (`vRP.request`) e campo de texto (`vRP.prompt`) ficam dentro do core. Adicione no
fim de `client_scripts` do `fxmanifest.lua` (ou `__resource.lua`) do `vrp`:

```lua
'@one_hud/bridge/vrp.lua'
```
{% endstep %}

{% step %}
### Se a sua base tem a pasta `hud`: importe o que tem jogo dentro

Muitas bases vRPex (lotus e derivados) colocam na HUD coisas que não são só tela: relógio e clima sincronizados
(`/hora`, `/dia`, `/noite`, `/clima`), cinto, nitro, capô, chamados de recrutamento (`/rec`), pontos e anúncios.
Para não perder nada, com o servidor ligado digite no **console do servidor**:

```
onehud_import
```

Depois tire `ensure hud` do `server.cfg`. Tudo continua funcionando, só que aparecendo no one\_hud.
{% endstep %}

{% step %}
### Desligue o resto das telas antigas

Tire do `server.cfg` as HUDs e notificações antigas que sobrarem (`vrp_hud`, `nation_hud`, `vrp_notify`...).
O evento `Notify` dos scripts (`sucesso`, `negado`, `aviso`, `importante`) passa a aparecer no one\_hud.
{% endstep %}

{% step %}
### Reinicie

`refresh` e reinicie o servidor.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

No console do servidor:

```
[one_hud] gameplay do HUD da base carregado (lotus)     ← só se você importou a hud
```

No F8 do jogo (ou com `/onehud`):

```
[one_hud] vrpex · gameplay do HUD: ok
```

## Observações

* **Fome e sede:** vêm do `vRP.getHunger/getThirst`. Se a sua base não tem fome/sede (muitas vRPex desligam), os
  dois anéis somem sozinhos.
* **Cinto:** com a HUD da base importada, vale o cinto dela (mesma tecla). Sem ela, o one\_hud liga o próprio (`B`).
* **Minimapa:** é do one\_hud (`Config.Minimap` e `Config.MinimapStyle`). Scripts que chamavam
  `exports.hud:setMapDisplayMode(...)` continuam funcionando.
* **Chamados de recrutamento:** aparecem como pedido do one\_hud; aceitar marca o local no mapa.
