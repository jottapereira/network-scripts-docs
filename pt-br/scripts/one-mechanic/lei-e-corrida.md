---
description: Regras de conformidade, vistoria, perícia, classes de corrida, sabotagem e drivetrain.
---

# Lei, perícia e corrida

## Regras de conformidade

Oito regras como dado (`content/rules.lua`): ruído, película, neon, altura, peso estrutural, blindagem, peça só de pista e peça pirata. Cada uma tem
gravidade, multa e consequência (`fine`, `noCert`, `impound`) e o dono liga ou desliga cada uma em `Config.Legality.rules`.

A **vistoria** (oficina com o módulo `legality` no tipo, como a oficial) varre o carro: sem infração bloqueadora, emite um **certificado** com validade.
Com `Config.Legality.requireCert = true`, `IsRoadLegal` devolve falso para carro sem certificado. **A Forja não multa nem apreende:** ela emite o evento
`forja:violation` e a polícia ou o tablet da cidade decide.

## Perícia

`/pericia` (grupos de polícia em `Config.Legality.policeGroups`), perto do carro, mostra:

* **hodômetro adulterado** (km do painel x km real), **desgaste incompatível** com o km, **VIN raspado**, **placa clonada**, roubado;
* rastros dos serviços clandestinos, peças com origem e série, oficinas que mexeram, infrações e se há vistoria;
* evidências de sabotagem, quando o módulo está ligado.

Os serviços clandestinos (raspar VIN, hodômetro, clonar placa) só existem em oficinas cujo tipo permite (`allow`), e **sempre deixam rastro**.

## Corridas

A Forja **não implementa corrida**: expõe o que as corridas precisam.

* **Classe** (D, C, B, A, S) pela potência medida no dinamômetro (`Config.Racing.classes`); o certificado vence se o carro rodar mais de 400 km depois.
* **Regulamento por evento:** `AllowsRace(placa, { maxClass, maxHp, noNitro, requireCert, clean })` devolve se passa e os motivos.
* **Ranking** do dinamômetro por classe. `/classe` mostra a classe do carro.

## Sabotagem (opcional, desligada por padrão)

É RP de investigação, não griefing: exige **ferramenta** (item), **tempo** e proximidade; leva o componente a "ruim", nunca a "falhou" sem
`Config.Sabotage.allowLethal`; e deixa **evidência com assinatura** do autor que a perícia lê. O staff vê tudo na auditoria.

## Drivetrain (opcional, experimental)

Câmbio manual com embreagem (`/cambio`), controle de tração (`/tracao`) e nitro com garrafa (`/nitro`, tecla). Roda por quadro só para o motorista com a função
ligada, em classes liberadas por `Config.Drivetrain`. O nitro é validado no servidor: carga no carro, consumo limitado pelo tempo, ganho pela qualidade do kit.
