---
description: Log no console, alertas de exploit e auditoria em webhook.
---

# Log

| Função | Descrição |
|---|---|
| `One.Log.Debug/Info/Warn/Error(msg, ...)` | console, com formatação (`%s`, `%d`) |
| `One.Log.Exploit(src, reason, data?)` | ação suspeita. Registra e envia para `one:webhook:exploit` |
| `One.Log.Audit(channel, src, message, data?)` | auditoria. Envia para `one:webhook:<channel>` |

```lua
One.Log.Exploit(src, 'tentou comprar item inexistente', { item = itemId })
One.Log.Audit('shop', src, 'Comprou água', { price = 6 })
```

{% hint style="info" %}
`Exploit` **não pune** o jogador: só registra. A punição é decisão do seu servidor.
{% endhint %}

O nível do console é definido por `set one:log_level "info"`. Outros sistemas de log podem escutar o evento
`one:server:log` (veja [Eventos](../eventos.md)).
