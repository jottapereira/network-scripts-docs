---
description: Servidor sem framework. Cerca de 3 minutos.
---

# Instalação: Standalone

```cfg
ensure oxmysql
ensure one_lib
ensure one_hud
```

Sem framework não há dinheiro, emprego nem fome/sede: esses elementos ficam escondidos até um script mandar os
valores. Vida, colete, fôlego, oxigênio, voz (pma-voice/SaltyChat), arma, velocímetro e minimapa funcionam sozinhos.

Seus scripts usam as telas pela [API](../integracoes.md) (`exports.one_hud:Notify`, `Progress`, `Input`...) ou pelo
[one\_lib](../../../one-lib/modulos/tela.md) (`One.Notify`, `One.Progress`...).
