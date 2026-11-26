---
description: Exports, eventos e filtros da Forja para integrar com outros scripts.
---

# Integração com outros scripts

## Exports (servidor)

| Export | Devolve |
|---|---|
| `GetVehicleState(placa)` | VIN, km, km real, vida de cada componente, peças, visual, bandeiras |
| `Scan(placa)` | Lista de infrações da legalidade |
| `IsRoadLegal(placa)` | `true` ou `false`, motivo (para licenciamento) |
| `GetForensics(placa)` | Relatório pericial (para o tablet da polícia) |
| `GetDynoCertificate(placa)` | Último certificado do dinamômetro |
| `GetClassCertificate(placa)` | Classe, cv, Nm (ou `nil` e o motivo) |
| `AllowsRace(placa, regulamento)` | Se o carro cumpre o regulamento do evento e os motivos |
| `Leaderboard(classe?, limite?)` | Ranking do dinamômetro |
| `SetFlag(placa, bandeira, ligado)` | Marca o carro como `STOLEN`, `SEIZED` ou `SCRAP` (polícia, desmanche) |
| `RegisterLiveryPack(pacote)` | Dá nome aos adesivos de modelos (pacotes de carros) |

```lua
local ok, motivos = exports.one_mechanic:AllowsRace('ABC1234', { maxClass = 'B', noNitro = true, requireCert = true })
```

## Eventos que a Forja dispara

`forja:violation` (placa, infrações), `forja:roadInspection`, `forja:orderDone`, `forja:partInstalled`, `forja:partRemoved`, `forja:dynoRun`, `forja:inspected`,
`forja:visualChanged`, `forja:wearState`, `forja:supplyDelivered`, `forja:vehicleDismantled`, `forja:skillLevel`, `forja:sabotage`.

```lua
AddEventHandler('forja:violation', function(plate, violations)
  -- sua multa, seu tablet
end)
```

## Filtros (modificam o resultado antes de acontecer)

`Forja.Filter('price', fn)` (preço de uma linha), `wear` (perdas do desgaste), `diagnosis` (achados), `partQuality` e `partBonus` (qualidade da peça),
`paintCap` (teto da pintura), `dyno` (curva), `shopAccess` (acesso à oficina), `lineDoneCheck` (marcar item como feito). Um filtro que falha é isolado:
o erro vai ao log e o fluxo segue com o valor original.

```lua
Forja.Filter('price', function(ctx)
  if ctx.shop.type == 'player' then ctx.parts = math.floor(ctx.parts * 0.9) end
  return ctx
end)
```
