---
description: Dinheiro em três contas normalizadas.
---

# Money

Contas: `cash` (espécie), `bank` (banco) e `dirty` (sujo). Valores são sempre **inteiros positivos**; o
módulo recusa qualquer outro valor antes de chegar ao framework.

| Função | Retorno |
|---|---|
| `One.Money.Get(src, account)` | saldo ou `nil` |
| `One.Money.Add(src, account, amount, reason?)` | `boolean` |
| `One.Money.Remove(src, account, amount, reason?)` | `boolean`. Só remove se houver saldo |
| `One.Money.Pay(src, amount, accounts?, reason?)` | conta usada ou `nil` |

`Pay` tenta as contas na ordem dada (padrão `{ 'cash', 'bank' }`) e cobra da primeira com saldo:

```lua
local paidWith = One.Money.Pay(src, 500)
if not paidWith then
    return One.Notify(src, 'Dinheiro insuficiente', 'error')
end
```

{% hint style="warning" %}
Nunca use um valor vindo do cliente como preço. Calcule o valor no servidor.
{% endhint %}

Conta não suportada pelo framework (ex.: `dirty` no QBCore) retorna `nil`/`false` e mostra um aviso no console uma única vez.
