---
description: Utilitários e validação de dados vindos do cliente.
---

# Utils

## Validação

Retornam o valor válido ou `nil`. Use em **todo** dado que vem do cliente ou da NUI.

| Função | Descrição |
|---|---|
| `One.Utils.Number(value, min?, max?, integer?)` | número dentro da faixa (rejeita `NaN` e infinito) |
| `One.Utils.String(value, maxLength?, pattern?)` | texto com tamanho máximo e padrão Lua opcional |

```lua
local amount = One.Utils.Number(data.amount, 1, 100, true)
if not amount then
    return One.Log.Exploit(src, 'quantidade inválida', data)
end
```

## Gerais

| Função | Descrição |
|---|---|
| `Round(value, decimals?)` | arredonda |
| `Clamp(value, min, max)` | limita à faixa |
| `Trim(text)` | remove espaços nas pontas |
| `Split(text, separator?)` | divide (padrão `,`) |
| `Count(tbl)` | quantidade de chaves |
| `Copy(value)` | cópia profunda |
| `Merge(base, override)` | mescla profunda sem alterar os originais |
