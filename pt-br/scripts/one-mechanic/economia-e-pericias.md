---
description: "Estoque, fornecedor, desmanche, fabricação, perícias, licenças: o RP em volta da oficina."
---

# Economia e perícias

## Peças como economia

| Fonte | Como funciona | Quem ganha RP |
|---|---|---|
| **Fornecedor** | A oficina pede peças novas e originais do catálogo, paga do caixa e recebe no prazo (`Config.Economy.deliveryMinutes`). O preço sobe com a procura recente e desce com o tempo | Donos de oficina, quem entrega |
| **Estoque** | Trocar uma peça numa ordem consome do estoque; sem peça, não marca como feito. O cliente também compra no ponto de estoque, com a margem da oficina | Lojistas |
| **Desmanche** | Em ferro-velho, carro sucateado, apreendido ou roubado (bandeira do carro) vira peças usadas, componentes aproveitados e sucata | Desmanche, ferro-velho |
| **Reciclagem** | Peça gasta vira sucata de metal | Cadeia de materiais |
| **Fabricação** | Receitas por peça (materiais no estoque, perícia de tuning): sai a peça artesanal | Mecânicos fabricantes |
| **Mercado de tunes** | O tuner grava o ajuste num chip e vende; a oficina cobra a instalação | Tuners famosos |

Tudo passa pelo servidor com baixa atômica de estoque e **trilha de auditoria** de cada movimento.

## Perícias

Seis perícias com XP e nível: motor, elétrica, funilaria, pintura, tuning, diagnóstico. XP vem do trabalho feito. Cada nível:

* sobe o **teto da nota de pintura** (`55 + 9 por nível`, nível 5 = 100);
* melhora a **qualidade das peças instaladas** (`+6% por nível de tuning`);
* libera **receitas** de fabricação.

**Mentoria:** o aprendiz com um chefe ou dono da mesma oficina a até 20 m ganha 50% mais XP e o mentor recebe 10%. `/pericias` mostra o resumo.
`Config.Skills.enabled = false` iguala todos.

## Licenças

Mecânico certificado, tuner licenciado (você define em `Config.Skills.licenses`). Emitidas pela oficina de um tipo autorizado a quem está perto, ou por
`forja_license`. Têm validade. Tipos de oficina com `requires` só aceitam quem tem a licença (o dono é isento).

