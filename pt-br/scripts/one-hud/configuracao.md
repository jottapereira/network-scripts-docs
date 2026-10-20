---
description: config.lua, fontes de dados e arquivos abertos.
---

# Configuração

## config.lua

| Opção | Padrão | O que faz |
|---|---|---|
| `Config.Brand` / `Config.Logo` | `'N1'` / `nil` | Marca no canto: texto curto ou imagem (`'nui://one_hud/web/logo.png'`) |
| `Config.Unit` | `'kmh'` | Velocidade em `kmh` ou `mph` |
| `Config.Minimap` | `'vehicle'` | Minimapa: `vehicle` (só dirigindo), `always` ou `never` |
| `Config.MinimapStyle` | `'circle'` | `circle`: redondo, como o HUD do vRP Creative (usa a máscara `circleminimap` se a base tiver o stream) · `square`: retângulo na moldura do design |
| `Config.CircleMinimap` | posições do Creative | Ajuste fino do minimapa redondo (coordenadas do GTA, zoom, textura da máscara) |
| `Config.Currency` | `'$'` | Símbolo do dinheiro |
| `Config.PlayerId` | `'server'` | Chip de ID: id do servidor (`server`) ou do personagem (`character`) |
| `Config.ShowId` / `ShowOnline` / `ShowJob` | `true` | Chips do topo |
| `Config.Temperature` | por clima | Temperatura exibida para cada clima (ambientação) |
| `Config.ToggleCommand` | `'hud'` | Comando para o jogador esconder/mostrar (`nil` = sem comando) |
| `Config.Keys` | `Y`, `N`, `X` | Aceitar e recusar pedido, cancelar progresso |
| `Config.NotifyDuration` | `5000` | Duração padrão das notificações (ms) |
| `Config.Voice` | `'auto'` | `pma-voice`, `saltychat`, `creative` ou `none` |
| `Config.Fuel` | `'auto'` | `ox_fuel`, `LegacyFuel`, `cdn-fuel`, `ps-fuel`, `lc_fuel` ou `native` |
| `Config.Seatbelt` | `'auto'` | `own` (cinto do one\_hud), `statebag`, `qb` ou `none` |
| `Config.OwnSeatbelt` | `B`, 55 km/h | Tecla, queda de velocidade que arremessa e trava da porta |
| `Config.Cruise` / `CruiseKey` | `false` / `J` | Limitador de velocidade |

`'auto'` detecta o que a base usa. O cinto próprio só liga quando a base não tem um (HUD do Creative,
qb-smallresources, qbx\_seatbelt).

## Arquivos abertos

| Arquivo | Para quê |
|---|---|
| `client/sources.lua` | De onde vem cada dado (status, voz, combustível, cinto, dinheiro) em cada base |
| `shared/weapons.lua` | Nome e modo das armas (quando o inventário/framework não informa) |
| `compat/client.lua` | Respostas no lugar de `esx_notify`, `esx_progressbar`, `esx_textui`, `progressbar`, `qb-input` e `Notify` |
| `bridge/*.lua` | Pontes de uma linha (qb-core, ox\_lib, vrp) |
| `extensions/creative/legacy.lua` | O que é importado do Creative, nomes dos chips, capacidade do nitro |
| `locales/*.lua` | Textos (pt-BR e en) |

## Idioma

Segue o idioma global do servidor (`setr one:locale "pt-BR"`) ou `Config.Locale`.
