---
description: Instalando o one_lib.
---

# Instalação

{% stepper %}
{% step %}
### Coloque o recurso

Extraia `one_lib` dentro de `resources`.
{% endstep %}

{% step %}
### Ordem no server.cfg

O `one_lib` precisa iniciar **depois** do framework e do `oxmysql`, e **antes** de qualquer produto `one_*`:

```cfg
ensure oxmysql
ensure es_extended      # ou qb-core, qbx_core, vrp...

ensure one_lib
ensure one_characters
```
{% endstep %}

{% step %}
### Confira a detecção

Ao iniciar, o console mostra:

```
[one_lib] v0.6.0 · framework: esx · aparência: illenium
```

Se algo estiver errado, force pelos [convars](convars.md).
{% endstep %}

{% step %}
### vRP Creative: interação (opcional, recomendado)

O one\_lib substitui o `target` (ALT) e o `hoverfy` ("Pressione E") da base, com marcas 3D e cartões de opções.
No console do servidor:

```
onelib_import_target
```

Depois tire `target` e `hoverfy` do `server.cfg`, rode `refresh` e reinicie. Detalhes em
[Interact](modulos/interact.md). Nas outras bases não há nada a fazer: com `ox_target` ou `qb-target`, a mira
continua sendo deles.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Atualizar o `one_lib` nunca exige mudar seus produtos: basta substituir a pasta e reiniciar o servidor.
{% endhint %}
