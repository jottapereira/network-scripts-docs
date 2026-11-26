---
description: Tudo que o dono da cidade configura na Forja.
---

# Configuração

Tudo fica em `config.lua` (aberto, fora do escrow) e em `content/` (dados). Cada bloco abaixo é uma tabela do `config.lua`.

| Bloco | Para que serve |
|---|---|
| `Config.Preset` | Preset da cidade: `arcade`, `balanced`, `realistic`, `hardcore` (ritmo do desgaste, preço, tempo de serviço, severidade dos sintomas) |
| `Config.Modules` | Liga e desliga cada módulo; dependente de módulo desligado é desligado também, com aviso |
| `Config.Vehicle` | `takeover`: `exclusive`, `coexist` ou `observe` com os scripts de carro da base |
| `Config.Core` | Intervalo de gravação em lote, tamanho do cache, intervalo da telemetria do motorista |
| `Config.Wear` | Ritmo global do desgaste, multiplicador por componente, sintomas ligados, carros sem dono |
| `Config.Pricing` | Forma de pagar (dinheiro por padrão) por categoria: peças, mão de obra, ajuste, visual |
| `Config.Shops` | Cargos por grau de emprego, limite de oficinas por dono, tempo de aprovação, comissão, tipos de ponto |
| `Config.Diagnosis` | Tempo de cada inspeção, precisão da vida mostrada, validade do relatório |
| `Config.Parts` | Tempo de instalação por minuto de mão de obra |
| `Config.TuneLimits` | Largura da faixa do ajuste fino por classe de veículo |
| `Config.Dyno`, `Config.Visual` | Duração da passada; minijogo de pintura e Mod Kit de desempenho |
| `Config.Economy` | Estoque nas ordens, preço de atacado, entrega, flutuação por demanda, reciclagem, desmanche |
| `Config.Skills` | Perícias ligadas, teto da pintura por nível, bônus de qualidade, mentoria, licenças |
| `Config.Legality`, `Config.Racing`, `Config.Sabotage` | Regras ligadas, vistoria obrigatória, classes de corrida, sabotagem |
| `Config.Roadside`, `Config.Drivetrain` | Reparo de rua e guincho; classes que usam câmbio manual, tração e nitro |
| `Config.Logs`, `Config.Audit` | O que entra na trilha de auditoria e por quantos dias |

## Presets

| Preset | Desgaste | Preço | Mão de obra | Sintomas |
|---|---|---|---|---|
| arcade | ×0,35 | ×0,8 | ×0,5 | ×0,6 |
| balanced | ×1,0 | ×1,0 | ×1,0 | ×1,0 |
| realistic | ×1,6 | ×1,2 | ×1,3 | ×1,2 |
| hardcore | ×2,5 | ×1,5 | ×1,8 | ×1,5 |

O painel da cidade (`/forja`, administração) mostra os módulos, o conteúdo carregado, conflitos com a base e um **simulador**:
quantas horas de direção a 60 km/h até cada peça gastar, para dirigir calmo, normal ou agressivo, e o preço da troca no preset ativo.
