---
description: vRP Creative v4/v5 (Three, Summerz e derivados). Cerca de 5 minutos.
---

# Instalação: vRP Creative v4/v5

Existem dois jeitos de HUD nessas bases, e o one\_hud reconhece os dois sozinho:

* **HUD em recurso `hud`** (Summerz e derivados): fome, sede, cinto, relógio e o chat ficam dentro do `hud`.
  Você roda um comando e o one\_hud traz esse "jogo" para dentro dele.
* **`vrp_hud` + `vrp_notify`** (Three e mais antigas): só desligar.

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

Deixe o HUD antigo ligado por enquanto: o próximo passo lê os arquivos dele.
{% endstep %}

{% step %}
### Base com recurso `hud`: importe o gameplay

Com o servidor ligado, digite no **console do servidor** (não no F8):

```
onehud_import
```

O console mostra quantos arquivos vieram. Eles ficam em `one_hud/extensions/creativev5/legacy/` e rodam isolados
dentro do one\_hud: fome e sede caindo, dano por fome/sede, estresse, oxigênio do mergulho, relógio (`/timeset`),
cinto, nitro, capuz, as perguntas do vRP (`prompt` e `request`) e os textos de interação. Tudo aparece no visual
do one\_hud.

Se a sua base não tem o recurso `hud`, o comando avisa e você pula para o próximo passo.
{% endstep %}

{% step %}
### Desligue o HUD antigo

* Base com recurso `hud`: tire `ensure hud` do `server.cfg`. **Ligue o chat do FiveM** (`ensure chat`), porque o
  chat dessas bases morava dentro do HUD antigo. As mensagens que os scripts mandam continuam chegando.
* Base com `vrp_hud`/`vrp_notify`: tire os dois do `server.cfg` (mantenha as pastas).

Rode `refresh` e reinicie o servidor.
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

* O evento `Notify` que os scripts disparam aparece no one\_hud com o tipo certo (`sucesso`, `negado`, `aviso`,
  `importante`).
* Fome e sede vêm do vRP.
* Sem cinto na base, o one\_hud liga o próprio (`B`).
* Esqueceu de importar? O console avisa a cada start: `código da base ("hud") não importado`.
* Esqueceu o `ensure chat`? O console avisa: `o chat desta base ficava no HUD antigo`.
