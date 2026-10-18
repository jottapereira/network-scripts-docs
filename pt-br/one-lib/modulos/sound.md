---
description: Sons de interface com os sons nativos dos menus do GTA.
---

# Sound

Os sons tocam pelo próprio jogo: soam como os menus do GTA, respeitam o volume de efeitos do jogador e não
exigem nenhum arquivo de áudio.

| Nome | Uso |
|---|---|
| `hover` | passar o mouse em algo interativo |
| `tick` | slider, stepper, troca rápida |
| `select` | clique / confirmar |
| `back` | voltar / cancelar |
| `error` | erro, validação recusada |
| `confirm` | ação importante concluída (ex.: segurar para confirmar) |
| `toggle` | ligar/desligar |

| Função | Descrição |
|---|---|
| `One.Sound.Play(name)` | toca o som |
| `One.Sound.Set(name, soundName, soundSet)` | troca o som de um gesto |
| `One.Sound.Enabled()` | `false` quando `setr one:sounds "false"` |
| `One.Sound.EnableNui()` | libera a NUI do recurso para pedir sons |

```lua
One.Sound.Set('confirm', 'WAYPOINT_SET', 'HUD_FRONTEND_DEFAULT_SOUNDSET')
```

O mesmo som não repete em menos de 35 ms, para nunca empilhar.
