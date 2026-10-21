---
description: Troque o verde da Network One pela cor da sua cidade, em todos os scripts ou em um só.
---

# Cor das telas

Todos os scripts vêm com o verde da Network One como cor de destaque (botões, seleção, barras, ícones ativos).
Você pode trocar por qualquer cor com **uma linha**.

## Em todos os scripts de uma vez

No `server.cfg`:

```cfg
setr one:accent "#ff6a00"
```

{% hint style="warning" %}
Use `setr` (com **r**): é o que deixa a cor chegar até a tela do jogador. Com `set` não funciona.
{% endhint %}

## Em um script só

No `config.lua` do script:

```lua
Config.Accent = '#ff6a00'
```

O `Config.Accent` do script vale mais que o `one:accent` do server.cfg. Deixe `nil` para usar a cor geral.

## Formatos aceitos

| Formato | Exemplo |
|---|---|
| Hex | `'#ff6a00'` ou `'#f60'` |
| RGB em texto | `'255, 106, 0'` |
| RGB em tabela (só no config.lua) | `{ 255, 106, 0 }` |

## O que você não precisa fazer

* **Tons de hover e escuros:** calculados a partir da sua cor.
* **Texto em cima da cor:** fica escuro em cores claras e branco em cores escuras, sempre legível.
* **Recompilar a interface:** não precisa. Reinicie o script (ou o servidor) e pronto.

Cores de aviso (vermelho de erro, amarelo de atenção) continuam as mesmas, para o jogador sempre reconhecer um
alerta.
