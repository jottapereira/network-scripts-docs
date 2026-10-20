---
description: vRP Creative (Network, Origens, Bewitched e derivadas). Cerca de 10 minutos.
---

# Instalação: vRP Creative

No Creative, o `hud` da base não é só tela: ele faz a fome e a sede caírem, o cinto e a ejeção, o nitro, os pneus
furando, o drift e os cronômetros de procurado/repouso. O one\_hud **importa esse gameplay da sua base** e roda
isolado, com o visual novo. Nada do Creative é enviado por nós: o código vem da **sua** pasta.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
start vrp

ensure one_lib
ensure one_hud

start [scripts]
```
{% endstep %}

{% step %}
### Importe o gameplay da sua base

Com o servidor ligado (e `hud` e `keyboard` ainda nas pastas), rode no **console do servidor**:

```
onehud_import
```

Copia o gameplay do `hud` e os formulários do `keyboard` para `one_hud/extensions/creative/legacy/`.
{% endstep %}

{% step %}
### Desligue os recursos antigos

Tire do `server.cfg` (ou mova para uma pasta que não inicia), **sem apagar as pastas**:

| Recurso | Substituído por |
|---|---|
| `hud` | HUD + gameplay importado |
| `notify` | notificações (evento `Notify`, mesmas cores) |
| `notifyitem` | aviso de item recebido/removido |
| `request` | pedidos `vRP.Request` (Y/N) |
| `keyboard` | formulários `vKEYBOARD.*` e `exports["keyboard"]:*` |
{% endstep %}

{% step %}
### Reinicie

`refresh` e reinicie o servidor inteiro.
{% endstep %}
{% endstepper %}

## Como saber que deu certo

```
[one_hud] extensão carregada: creative
[one_hud] gameplay do HUD da base carregado
```

Em jogo: fome e sede descendo com o tempo; `G` coloca o cinto (ícone verde no velocímetro); comandos de admin
abrem o formulário novo; pedidos aparecem à esquerda com Y/N.

## Observações

* `exports["hud"]:Wanted` / `Reposed` continuam respondendo para os scripts da base.
* O nitro aparece como arco azul embaixo do velocímetro. A capacidade máxima usada para a barra fica em
  `extensions/creative/legacy.lua` (`nitroMax`).
* Procurado, repouso, sorte, destreza, diamantes, cupom, roubos e safezone viram **chips** acima dos anéis
  (nomes e ícones em `legacy.lua`).
