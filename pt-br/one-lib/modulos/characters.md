---
description: Listar, criar, entrar e excluir personagens em qualquer framework.
---

# Characters

Módulo usado por sistemas de seleção de personagem (como o `one_characters`).

| Função | Retorno |
|---|---|
| `One.Characters.Supported` | `false` quando o framework não tem suporte a personagens |
| `GetSlots(src)` | slots da conta pelo framework, ou `nil` |
| `List(src)` | personagens da conta |
| `Owns(src, charId)` | o personagem pertence à conta e não foi excluído |
| `Create(src, data)` | **cria e entra**. Retorna o `charId` já carregado, ou `nil` |
| `Login(src, charId)` | entra num personagem existente |
| `Delete(src, charId)` | exclui (de forma recuperável onde o framework permite) |
| `GiveStarterItems(src, charId)` | itens iniciais do framework |

Cada personagem da lista:

```lua
{
    charId = '2', firstName = 'Lamar', lastName = 'Davies', sex = 'm',
    dob = '1994-03-12', phone = '555-0192', cash = 2430, bank = 48910,
    job = { name = 'mechanic', label = 'Mecânico', gradeLabel = 'Chefe' },
    lastLogin = 1760000000, position = { x = 0.0, y = 0.0, z = 0.0 }
}
```

`data` de `Create`: `{ firstName, lastName, sex = 'm'|'f', dob = 'YYYY-MM-DD', nationality, bio, model }`.

{% hint style="warning" %}
Sempre confira `Owns(src, charId)` antes de usar um `charId` que veio do cliente.
{% endhint %}
