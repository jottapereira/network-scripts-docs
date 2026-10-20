---
description: Escolha a sua base e siga o passo a passo. Cada guia leva de 5 a 10 minutos.
---

# Instalação

O one\_hud funciona em qualquer base suportada pelo [one\_lib](../../../one-lib/README.md). O que muda de uma base para
outra é **o que desligar** e se é preciso **uma linha** no core da base para as telas que moram dentro dele.

| Base | Guia | Desligar | Linha no core |
|---|---|---|---|
| vRP Creative | [Creative](creative.md) | `hud`, `notify`, `notifyitem`, `request`, `keyboard` | — |
| Creative v4/v5 | [Creative v4/v5](creative-v5.md) | HUD e notify da base | `vrp` (opcional) |
| vRPex / vRP 1 | [vRPex](vrpex.md) | HUD e notify da base | `vrp` (opcional) |
| ESX Legacy | [ESX](esx.md) | `esx_hud`, `esx_notify`, `esx_progressbar`, `esx_textui` | — |
| QBCore | [QBCore](qbcore.md) | `qb-hud`, `progressbar`, `qb-input` | `qb-core` |
| Qbox | [Qbox](qbox.md) | `qbx_hud` | `ox_lib` |
| Standalone | [Standalone](standalone.md) | — | — |

## Comum a todas as bases

* **Requisitos:** [`one_lib`](../../../one-lib/instalacao.md) **0.6 ou mais novo**, iniciado antes.
* **Ordem no `server.cfg`:**

```cfg
ensure oxmysql
ensure <seu framework>

ensure one_lib
ensure one_hud

# depois: os demais scripts
```

{% hint style="warning" %}
**Desligar não é apagar a pasta.** O one\_hud se apresenta com o nome dos recursos que substitui (`provide`) e
responde pelos exports deles; algumas bases conferem se a pasta existe. Deixe as pastas; só não dê `ensure`.
{% endhint %}

## A "linha no core"

Algumas telas moram **dentro** do framework (a notificação do QBCore está no qb-core; todo o ox\_lib é um recurso
só). Nesses casos não há o que desligar: uma linha no `fxmanifest.lua` do core redireciona as telas para o one\_hud.
Com o one\_hud parado, tudo volta ao original; para desfazer, apague a linha.

```lua
client_scripts {
    -- ... o que já estava aqui ...
    '@one_hud/bridge/qb-core.lua'      -- ou ox_lib.lua, ou vrp.lua
}
```

## Depois de instalar

1. Entre no servidor: a HUD aparece depois que o personagem carrega.
2. `/hud` esconde e mostra.
3. Ajuste em [Configuração](../configuracao.md).

## Teclas padrão

| Tecla | Ação |
|---|---|
| `Y` / `N` | aceitar / recusar pedido |
| `X` | cancelar progresso |
| `B` | cinto (só quando a base não tem um próprio) |
| `J` | limitador de velocidade (se ligado em `Config.Cruise`) |

O jogador troca todas em **Configurações > Atalhos > FiveM**.
