---
description: Como o carro desgasta, o que o jogador vê e como o mecânico descobre o problema.
---

# Desgaste e diagnóstico

## Desgaste

* O **motorista mede** a 1 Hz (distância, giro alto, freada forte, derrapagem, fora de estrada, batida, calor, água, nitro) e **envia a cada 30 s**.
  Carro parado, de NPC ou sem motorista não conta e não custa nada.
* O **servidor valida** (só o motorista daquele carro, ritmo de envio, velocidade possível) e converte em desgaste pela vida em km de cada componente,
  o ritmo do preset e o estresse (giro, freio, derrapagem, calor...). Valor impossível é cortado e vai para a auditoria.
* **Batida** estraga na hora só as peças sensíveis a impacto (radiador, suspensão).
* Cada componente cai por quatro estados: **em dia, gasto, ruim, falhou**; os limites vêm do preset.
* Carros sem dono na base não desgastam por padrão (`Config.Wear.trackUnowned`).

## O que o jogador comum vê

Nada de números: **luzes no painel** (injeção, óleo, temperatura, bateria, freios, transmissão, pneus, suspensão), **fumaça no capô**, e os
**sintomas**: perda de potência, freio longo, aderência, falha de ignição, motor que apaga, partida que falha. O carro **superaquece** com o radiador
ruim e fica inutilizável até esfriar, sem estragar a saúde real do motor. Isso dá motivo para o mecânico existir.

## Diagnóstico (nada aparece antes de inspecionado)

| Método | O que revela |
|---|---|
| **A olho, por zona** | Cofre do motor, dianteira, traseira, parte de baixo: peças visíveis ali, com a vida arredondada (`Config.Diagnosis.precision`) |
| **Scanner OBD** | Códigos das peças ruins ou falhas; marca como "pendente" as apenas gastas |
| **Alinhador 3D** | Alinhamento e suspensão |
| **Dinamômetro** | Defeitos pela forma da curva (velas, embreagem, filtro) |

Cada método tem um **tempo mínimo que o servidor exige**, com barra de progresso. O resultado entra no **relatório de inspeção** do carro: carimbo da
oficina, validade em dias e em km, e vale em outra oficina (`Config.Diagnosis.shareReports`). Cada achado vira um botão "Trocar" que põe a peça na ordem.

## Reparo de rua

Itens como dado em `content/items.lua`: kit de motor, cabos de chupeta, estepe. Levam o componente só até um **teto** (o reparo de rua nunca deixa
o carro novo) e exigem motor desligado. `/guincho` avisa a equipe das oficinas online; quem aceita recebe a rota no mapa. A pane seca fica com o
script de combustível da base.
