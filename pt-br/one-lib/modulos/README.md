---
description: Referência de todos os módulos do one_lib.
---

# Módulos

Todo módulo é acessado pelo global `One` e carregado **na primeira vez que é usado**.

```lua
-- fxmanifest.lua do seu script
shared_script '@one_lib/init.lua'
```

```lua
local name = One.Player.GetName(source)   -- carrega One.Player na primeira chamada
```

| Módulo | Lado | Para quê |
|---|---|---|
| [Player](player.md) | servidor · cliente | identidade do personagem e ciclo de vida |
| [Money](money.md) | servidor | dinheiro em espécie, banco e sujo |
| [Gems](gems.md) | servidor | moeda premium: da base, de um item ou do seu sistema |
| [Groups](groups.md) | servidor | empregos, gangues e grupos |
| [Callback](callback.md) | servidor · cliente | pedir e responder dados com rate limit |
| [Notify](notify.md) | servidor · cliente | notificações no sistema do servidor |
| [Locale](locale.md) | servidor · cliente | textos traduzíveis |
| [DB](db.md) | servidor | banco de dados e migrações |
| [Log](log.md) | servidor | console, exploits e auditoria em webhook |
| [RateLimit](ratelimit.md) | servidor | limite de frequência por jogador |
| [Cache](cache.md) | cliente | ped, veículo, assento e arma sem loop próprio |
| [Focus](focus.md) | cliente | foco de NUI sem conflito entre telas |
| [Sound](sound.md) | cliente | sons de interface nativos do GTA |
| [Appearance](appearance.md) | todos | aparência normalizada |
| [Characters](characters.md) | servidor | listar, criar, entrar e excluir personagens |
| [Utils](utils.md) | todos | utilitários e validação de entrada |
