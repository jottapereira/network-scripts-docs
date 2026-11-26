---
description: Peças de desempenho com origem e qualidade, ajuste fino, chips de ajuste e dinamômetro.
---

# Peças, ajuste e dinamômetro

## Peças

São 15 peças de desempenho em slots (turbo, ECU, escape, admissão, intercooler, embreagem, diferencial, freios, suspensão, estabilizadoras, peso, pneus, nitro).
Cada uma é um **item** com variantes por **origem**:

| Origem | Item | Qualidade | Vida inicial |
|---|---|---|---|
| Nova | `turbo_street` | 80–100 | cheia |
| Original | `turbo_street_oem` | 70–85 | cheia |
| Recondicionada | `turbo_street_refurb` | 55–75 | média |
| Artesanal | `turbo_street_crafted` | 50–95 | alta |
| Usada | `turbo_street_used` | 40–80 | baixa |
| Pirata | `turbo_street_pirate` | 25–60 | baixa (ilegal) |

A qualidade e a vida **saem sorteadas no servidor** na instalação, com bônus da perícia do mecânico. A peça só entra no carro depois da **instalação**
(barra de progresso, ponto de trabalho, cargo `tune`). Algumas peças exigem outras antes (turbo de pista pede ECU e intercooler). Ao retirar, a peça
volta ao inventário como **usada**. A peça instalada **desgasta com os km** e impõe estresse aos componentes (turbo gasta mais óleo e radiador).

## Pipeline de handling

O servidor calcula um **perfil** de fatores (peças pela eficácia, ajuste fino, sintomas do desgaste) com uma **faixa dura** por campo: nenhum conjunto
de peças passa do limite. O dono do carro aplica o perfil lendo o handling base ele mesmo, então funciona em qualquer modelo, inclusive de pacote.

## Ajuste fino

16 campos (potência, velocidade máxima, câmbio, freio, aderência, suspensão, estabilizadora, direção). Cada campo **precisa da peça do slot**; a faixa
encolhe pela classe do carro (`Config.TuneLimits`). Perfis prontos: **rua, arrancada, drift, pista**. O servidor valida tudo-ou-nada.

**Chip de ajuste:** grava o perfil num item com a assinatura do tuner. Só aplica em carro com as **mesmas peças**, pode ser travado ao VIN e só é usado
dentro de uma oficina onde o jogador tem o cargo `tune`.

## Dinamômetro

A curva é **calculada no servidor** com o mesmo perfil; o cliente anima os rolos. Os defeitos aparecem pela forma da curva e entram no relatório de
inspeção. O resultado vira **certificado** por placa (pico de cv e Nm, rpm, curva). A régua é a do Forja (`fInitialDriveForce × 900`), consistente entre
carros, não a potência real do GTA.
