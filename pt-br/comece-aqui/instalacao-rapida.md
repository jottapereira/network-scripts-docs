---
description: Do download ao primeiro login em menos de cinco minutos.
---

# Instalação rápida

{% stepper %}
{% step %}
### Baixe pelo Keymaster

Depois da compra, seus produtos aparecem em [keymaster.fivem.net](https://keymaster.fivem.net) na conta
Cfx.re usada na compra. Baixe o produto e o `one_lib`.
{% endstep %}

{% step %}
### Coloque na pasta resources

Extraia as pastas `one_lib` e `one_<produto>` dentro de `resources` (pode ser numa categoria, como `[one]`).
{% endstep %}

{% step %}
### Adicione ao server.cfg

Sempre **depois** do framework e do `oxmysql`, e o `one_lib` antes de qualquer produto:

```cfg
ensure oxmysql
ensure seu_framework

ensure one_lib
ensure one_characters
```
{% endstep %}

{% step %}
### Desative o sistema equivalente

Se o produto substitui algo que sua base já tem (por exemplo, a seleção de personagem), desative o antigo.
Cada produto tem uma tabela "o que desativar" por framework na sua página de instalação.
{% endstep %}

{% step %}
### Inicie e confira

As tabelas do banco são criadas sozinhas no primeiro start. No console deve aparecer:

```
[one_lib] v0.6.0 · framework: <seu framework> · aparência: <seu sistema de roupa>
```

Pronto. Entre no servidor e teste.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Se o framework detectado estiver errado, force pelo `server.cfg`: `setr one:framework "esx"`.
Veja todas as opções em [Convars](../one-lib/convars.md).
{% endhint %}
