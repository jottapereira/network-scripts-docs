---
description: Foco de NUI sem duas telas disputando o mouse e o teclado.
---

# Focus

```lua
-- abrir
One.Focus.Set(true)                          -- cursor visível, jogo sem input
One.Focus.Set(true, { keepInput = true })    -- o jogador continua andando

-- fechar
One.Focus.Set(false)
```

| Função | Descrição |
|---|---|
| `One.Focus.Set(enabled, opts?)` | `opts.cursor` (padrão `true`), `opts.keepInput` (padrão `false`) |
| `One.Focus.IsBusy()` | `true` se **outro** recurso está com uma tela aberta |

```lua
if One.Focus.IsBusy() then return end   -- não abrir por cima de outra tela
```

O registro de foco é liberado sozinho se o recurso que o tinha for parado.
