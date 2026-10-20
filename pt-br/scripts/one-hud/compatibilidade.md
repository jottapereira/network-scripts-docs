---
description: O que o one_hud substitui em cada base e como.
---

# Compatibilidade

| Tela | Creative | Creative v4/v5 · vRPex | ESX | QBCore | Qbox / ox\_lib |
|---|---|---|---|---|---|
| HUD | `hud` (gameplay importado) | HUD da base | `esx_hud` | `qb-hud` | `qbx_hud` |
| Notificação | `notify` | `Notify` · ponte `vrp` | `esx_notify` | ponte `qb-core` | ponte `ox_lib` |
| Progresso | `Progress` | — | `esx_progressbar` | `progressbar` + ponte `qb-core` | ponte `ox_lib` |
| Formulário | `keyboard` | ponte `vrp` (`prompt`) | — | `qb-input` | ponte `ox_lib` |
| Confirmação | — | — | — | — | ponte `ox_lib` |
| Pedido Y/N | `request` | ponte `vrp` (`request`) | — | — | — |
| Texto de ajuda | `hoverfy` (one\_lib) | — | `esx_textui` | ponte `qb-core` (`DrawText`) | ponte `ox_lib` |
| Item recebido | `notifyitem` | — | — | — | — |

Sem "ponte" = basta desligar o original (mantendo a pasta). "Ponte" = uma linha no `fxmanifest.lua` daquele recurso.

## Dados por base

| Dado | Fonte |
|---|---|
| Fome/sede/estresse | Creative: eventos do servidor · QB/Qbox: metadata e statebags · ESX: `esx_status` · vRP: lido a cada 15 s |
| Voz | pma-voice, SaltyChat, forks do Creative |
| Combustível | ox\_fuel, LegacyFuel, cdn-fuel, ps-fuel, lc\_fuel ou native |
| Cinto | HUD do Creative, qb-smallresources, qbx\_seatbelt, statebag `seatbelt` ou o próprio |
| Dinheiro/emprego | eventos do framework + conferência a cada 3 s / 30 s |
| Nome da arma | one\_inventory, `QBCore.Shared.Weapons`, `ESX.GetWeaponLabel`, `shared/weapons.lua` |

## Fora desta versão

Menu de contexto (`dynamic`, `esx_context`, `qb-menu`, `lib.registerContext`), skill check e chamados da polícia
continuam com as telas da base.
